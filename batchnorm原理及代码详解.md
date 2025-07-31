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
