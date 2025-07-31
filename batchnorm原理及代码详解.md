# batchnorm原理及代码详解
参考链接：https://blog.csdn.net/qq_25737169/article/details/79048516

## Batchnorm引入背景
### Internal Covariate Shift
google小组《Batch Normalization》提出，主要描述：训练深度网络的时候经常发生训练困难的问题，因为，每一次参数迭代更新后，上一层网络的输出数据经过这一层网络计算后，数据的分布会发生变化，为下一层网络的学习带来困难（神经网络本来就是要学习数据的分布，要是分布一直在变，学习就很难了），此现象称之为Internal Covariate Shift

Batch NormalizatoinNormalizatoin 之前的解决方案就是使用较小的学习率，和小心的初始化参数，对数据做白化处理，但是显然治标不治本。

### covariate shift
covariate shift主要描述：由于训练数据和测试数据存在分布的差异性，给网络的泛化性和训练速度带来了影响，我们经常使用的方法是做归一化或者白化。
<img width="1220" height="314" alt="image" src="https://github.com/user-attachments/assets/1b5234f0-75ba-4ba7-9125-c7f5b0336a31" />
举个简单线性分类栗子，假设我们的数据分布如a所示，参数初始化一般是0均值，和较小的方差，此时拟合的y = w x + b y=wx+by=wx+b如b图中的橘色线，经过多次迭代后，达到紫色线，此时具有很好的分类效果，
但是如果我们将其归一化到0点附近，显然会加快训练速度，如此我们更进一步的通过变换拉大数据之间的相对差异性，那么就更容易区分了。
 

## Batchnorm原理解读
* 直接对每层的输出后的数据归一化到0均值，1方差的正态分布，会造成每一层的数据分布都是正态分布，导致完全学习不到输入数据的特征，因此直接对每一层归一化不合理；
* 加入可训练的参数做归一化，如下图所示就是Batch Norm的实现，最大区别就是引入了平移参数和缩放参数来保证每一次数据归一化后，依然可以保留学习到的特征，同时完成归一化加速训练；
<img width="521" height="424" alt="image" src="https://github.com/user-attachments/assets/01154753-e38f-43db-9782-4d111c4fabaa" />

def Batchnorm_simple_for_train(x, gamma, beta, bn_param):
"""
param:x    : 输入数据，设shape(B,L)
param:gama : 缩放因子  γ
param:beta : 平移因子  β
param:bn_param   : batchnorm所需要的一些参数
	eps      : 接近0的数，防止分母出现0
	momentum : 动量参数，一般为0.9， 0.99， 0.999
	running_mean ：滑动平均的方式计算新的均值，训练时计算，为测试数据做准备
	running_var  : 滑动平均的方式计算新的方差，训练时计算，为测试数据做准备
"""
	running_mean = bn_param['running_mean']  #shape = [B]
    running_var = bn_param['running_var']    #shape = [B]
	results = 0. # 建立一个新的变量
    
	x_mean=x.mean(axis=0)  # 计算x的均值
    x_var=x.var(axis=0)    # 计算方差
    x_normalized=(x-x_mean)/np.sqrt(x_var+eps)       # 归一化
    results = gamma * x_normalized + beta            # 缩放平移

    running_mean = momentum * running_mean + (1 - momentum) * x_mean
    running_var = momentum * running_var + (1 - momentum) * x_var
    
    #记录新的值
    bn_param['running_mean'] = running_mean
    bn_param['running_var'] = running_var 
    
	return results , bn_param


def Batchnorm_simple_for_test(x, gamma, beta, bn_param):
"""
param:x    : 输入数据，设shape(B,L)
param:gama : 缩放因子  γ
param:beta : 平移因子  β
param:bn_param   : batchnorm所需要的一些参数
	eps      : 接近0的数，防止分母出现0
	momentum : 动量参数，一般为0.9， 0.99， 0.999
	running_mean ：滑动平均的方式计算新的均值，训练时计算，为测试数据做准备
	running_var  : 滑动平均的方式计算新的方差，训练时计算，为测试数据做准备
"""
	running_mean = bn_param['running_mean']  #shape = [B]
    running_var = bn_param['running_var']    #shape = [B]
	results = 0. # 建立一个新的变量
   
    x_normalized=(x-running_mean )/np.sqrt(running_var +eps)       # 归一化
    results = gamma * x_normalized + beta            # 缩放平移
    
	return results , bn_param


 ## Batchnorm源码解读
 def batch_norm_layer(x, train_phase, scope_bn):
    with tf.variable_scope(scope_bn):
		# 新建两个变量，平移、缩放因子
        beta = tf.Variable(tf.constant(0.0, shape=[x.shape[-1]]), name='beta', trainable=True)
        gamma = tf.Variable(tf.constant(1.0, shape=[x.shape[-1]]), name='gamma', trainable=True)
        
        # 计算此次批量的均值和方差
        axises = np.arange(len(x.shape) - 1)
        batch_mean, batch_var = tf.nn.moments(x, axises, name='moments')

		# 滑动平均做衰减
        ema = tf.train.ExponentialMovingAverage(decay=0.5)

        def mean_var_with_update():
            ema_apply_op = ema.apply([batch_mean, batch_var])
            with tf.control_dependencies([ema_apply_op]):
                return tf.identity(batch_mean), tf.identity(batch_var)
        # train_phase 训练还是测试的flag
		# 训练阶段计算runing_mean和runing_var，使用mean_var_with_update（）函数
		# 测试的时候直接把之前计算的拿去用 ema.average(batch_mean)
        mean, var = tf.cond(train_phase, mean_var_with_update,
                            lambda: (ema.average(batch_mean), ema.average(batch_var)))
        normed = tf.nn.batch_normalization(x, mean, var, beta, gamma, 1e-3)
    return normed

  ## Batchnorm缺点
  * 没有它之前，需要小心的调整学习率和权重初始化，但是有了BN可以放心的使用大学习率，但是使用了BN，就不用小心的调参了，较大的学习率极大的提高了学习速度，
  * Batchnorm本身上也是一种正则的方式，可以代替其他正则方式如dropout等
  * 另外，个人认为，batchnorm降低了数据之间的绝对差异，有一个去相关的性质，更多的考虑相对差异性，因此在分类任务上具有更好的效果。
  * 或许大家都知道了，韩国团队在2017NTIRE图像超分辨率中取得了top1的成绩，主要原因竟是去掉了网络中的batchnorm层，由此可见，BN并不是适用于所有任务的，在image-to-image这样的任务中，尤其是超分辨率上，图像的绝对差异显得尤为重要，所以batchnorm的scale并不适合。
