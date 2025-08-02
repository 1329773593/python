tqdm 是 Python 中用于显示进度条的强大工具，其核心参数可分为 进度控制、显示样式 和 高级功能 三类。以下是所有关键参数的详解和示例：

一、进度控制参数

参数 类型 作用 示例

iterable 可迭代对象 要遍历的数据源（如列表、DataLoader） tqdm([1,2,3])

total int 总迭代次数（未提供时自动推断） total=len(dataloader)

desc str 进度条左侧描述文字 desc="Training"

leave bool 完成后是否保留进度条 leave=False（完成后消失）

position int 多进度条时的垂直位置（0开始） position=1（第2行）

示例：
from tqdm import tqdm
import time

data = range(100)
for i in tqdm(data, total=100, desc="Processing", leave=True):
    time.sleep(0.1)  # 模拟任务


二、显示样式参数

参数 类型 作用 示例

ncols int 进度条总宽度（字符数） ncols=80

ascii bool/str 使用ASCII字符替代默认动画 ascii=" ▖▘▝▗▚▞█"

colour str 进度条颜色（需终端支持） colour="green"

bar_format str 自定义进度条格式 "{l_bar}{bar:20}{r_bar}"

dynamic_ncols bool 自动调整宽度适应终端 dynamic_ncols=True

自定义样式示例：
bar = tqdm(data, ncols=100, colour="#00ff00", 
           bar_format="{l_bar}{bar:20}{r_bar}{postfix}")


三、时间/速度参数

参数 类型 作用 示例

unit str 迭代单位名称 unit="img"

unit_scale bool/int 自动缩放单位（如K/M/G） unit_scale=True

mininterval float 进度条最小刷新间隔（秒） mininterval=0.5

maxinterval float 进度条最大刷新间隔（秒） maxinterval=10

示例（显示处理速度）：
tqdm(data, unit="samples", unit_scale=True, mininterval=0.1)
# 输出：50%|█████     | 500/1000 [00:05<00:05, 98.00samples/s]


四、文件/输出控制

参数 类型 作用 示例

file file-like 输出流（默认sys.stderr） file=sys.stdout

disable bool 禁用进度条（用于日志模式） disable=not verbose

gui bool 启用GUI模式（如Jupyter） gui=True

重定向输出示例：
import sys
with open('log.txt', 'w') as f:
    for i in tqdm(data, file=f):  # 进度条写入文件
        ...


五、动态控制方法

通过返回的 tqdm 对象可实时调整：
方法 作用 示例

set_description() 修改左侧描述 pbar.set_description("Epoch %d" % epoch)

set_postfix() 在右侧追加信息 pbar.set_postfix(loss=loss.item())

update() 手动更新进度 pbar.update(10)（前进10步）

refresh() 强制刷新显示 pbar.refresh()

close() 提前关闭进度条 pbar.close()

动态更新示例：
pbar = tqdm(total=100)
for i in range(10):
    pbar.update(10)
    pbar.set_postfix(loss=i*0.1)
pbar.close()


六、特殊场景参数

参数 适用场景 示例

smoothing 速度估算平滑系数（0~1） smoothing=0.3（更稳定）

initial 初始进度值 initial=50（从50开始）

lock_args 多线程时锁定参数 lock_args=(True, False)

完整代码示例

from tqdm import tqdm
import time, random

# 复杂参数组合
pbar = tqdm(
    range(100),
    total=100,
    desc="Training",
    ncols=100,
    unit="batch",
    unit_scale=True,
    colour="#FFA500",
    bar_format="{l_bar}{bar:20}{r_bar}{postfix}",
    postfix={"loss": "N/A"}
)

for i in pbar:
    time.sleep(0.1)
    if i % 10 == 0:
        pbar.set_postfix(loss=random.random())  # 动态更新损失


注意事项

1. Jupyter环境：需改用 from tqdm.notebook import tqdm
2. 多进度条冲突：通过 position 参数错开显示位置
3. 性能影响：在超高频迭代中建议设置 mininterval=0.1 降低刷新频率

掌握这些参数后，可以精准控制进度条在各种场景下的显示效果！
