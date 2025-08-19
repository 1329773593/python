# Python 中不同数据类型转为 NumPy 数组的方法及示例

在 Python 中，将各种数据类型转换为 NumPy 数组有多种方法。以下是常见数据类型转换的详细指南和示例：

## 1. Python 基本数据类型

### 1.1 列表 (List) → NumPy 数组

```
import numpy as np

# 一维列表
list_1d = [1, 2, 3, 4, 5]
array_1d = np.array(list_1d)
print(array_1d)  # 输出: [1 2 3 4 5]

# 二维列表
list_2d = [[1, 2, 3], [4, 5, 6]]
array_2d = np.array(list_2d)
print(array_2d)
# 输出:
# [[1 2 3]
#  [4 5 6]]
```

### 1.2 元组 (Tuple) → NumPy 数组

```
tuple_data = (1, 2, 3, 4, 5)
array_from_tuple = np.array(tuple_data)
print(array_from_tuple)  # 输出: [1 2 3 4 5]
```

### 1.3 集合 (Set) → NumPy 数组

```
set_data = {1, 2, 3, 4, 5}
array_from_set = np.array(list(set_data))  # 需要先转换为列表
print(array_from_set)  # 输出: [1 2 3 4 5] (顺序可能不同)
```

### 1.4 字典 (Dict) → NumPy 数组

```
dict_data = {'a': 1, 'b': 2, 'c': 3}

# 转换键
keys_array = np.array(list(dict_data.keys()))
print(keys_array)  # 输出: ['a' 'b' 'c']

# 转换值
values_array = np.array(list(dict_data.values()))
print(values_array)  # 输出: [1 2 3]
```

## 2. 科学计算库数据类型

### 2.1 PyTorch 张量 → NumPy 数组

```
import torch

torch_tensor = torch.tensor([1, 2, 3])
numpy_array = torch_tensor.numpy()  # 方法1：使用 .numpy() 方法
# 或者
numpy_array = np.array(torch_tensor)  # 方法2：使用 np.array()

print(numpy_array)  # 输出: [1 2 3]
```

### 2.2 TensorFlow 张量 → NumPy 数组

```
import tensorflow as tf

tf_tensor = tf.constant([1, 2, 3])
numpy_array = tf_tensor.numpy()  # 方法1：使用 .numpy() 方法
# 或者
numpy_array = np.array(tf_tensor)  # 方法2：使用 np.array()

print(numpy_array)  # 输出: [1 2 3]
```

### 2.3 SciPy 稀疏矩阵 → NumPy 数组

```
from scipy import sparse

sparse_matrix = sparse.csr_matrix([[1, 0, 0], [0, 2, 0]])
dense_array = sparse_matrix.toarray()  # 转换为密集数组

print(dense_array)
# 输出:
# [[1 0 0]
#  [0 2 0]]
```

## 3. 数据分析库数据类型

### 3.1 Pandas Series → NumPy 数组

```
import pandas as pd

series = pd.Series([1, 2, 3, 4])
numpy_array = series.to_numpy()  # 推荐方法
# 或者
numpy_array = series.values  # 旧方法（仍可用）
# 或者
numpy_array = np.array(series)

print(numpy_array)  # 输出: [1 2 3 4]
```

### 3.2 Pandas DataFrame → NumPy 数组

```
df = pd.DataFrame({'A': [1, 2], 'B': [3, 4]})
numpy_array = df.to_numpy()  # 推荐方法
# 或者
numpy_array = df.values  # 旧方法（仍可用）
# 或者
numpy_array = np.array(df)

print(numpy_array)
# 输出:
# [[1 3]
#  [2 4]]
```

## 4. 其他数据类型

### 4.1 生成器 (Generator) → NumPy 数组

```
gen = (x for x in range(5))
numpy_array = np.fromiter(gen, dtype=int)  # 使用 np.fromiter()

print(numpy_array)  # 输出: [0 1 2 3 4]
```

### 4.2 字符串 → NumPy 数组

```
text = "hello"
char_array = np.array(list(text))  # 转换为字符数组
print(char_array)  # 输出: ['h' 'e' 'l' 'l' 'o']

# 或者使用特定数据类型
byte_array = np.frombuffer(text.encode(), dtype=np.uint8)
print(byte_array)  # 输出: [104 101 108 108 111] (ASCII 码)
```

### 4.3 图像数据 (PIL Image) → NumPy 数组

```
from PIL import Image

# 创建示例图像
img = Image.new('RGB', (2, 2), color='red')
img_array = np.array(img)

print(img_array.shape)  # 输出: (2, 2, 3)
print(img_array)
# 输出:
# [[[255   0   0]
#   [255   0   0]]
#  [[255   0   0]
#   [255   0   0]]]
```

## 5. 高级转换技巧

### 5.1 指定数据类型

```
float_list = [1.1, 2.2, 3.3]
int_array = np.array(float_list, dtype=np.int32)  # 转换为整数
print(int_array)  # 输出: [1 2 3]
```

### 5.2 创建视图而非副本

```
original = [1, 2, 3]
array_view = np.asarray(original)  # 创建视图（如果可能）

array_view[0] = 10
print(original)  # 输出: [10, 2, 3] (原始数据被修改)
```

### 5.3 结构化数组

```
data = [('Alice', 25, 55.5), ('Bob', 30, 75.0)]
dtype = [('name', 'U10'), ('age', 'i4'), ('weight', 'f4')]
struct_array = np.array(data, dtype=dtype)

print(struct_array)
# 输出: [('Alice', 25, 55.5) ('Bob', 30, 75.0)]
```

## 总结表

| 数据类型         | 转换方法                        | 示例                               |
| ---------------- | ------------------------------- | ---------------------------------- |
| Python 列表      | `np.array(list)`                | `np.array([1, 2, 3])`              |
| Python 元组      | `np.array(tuple)`               | `np.array((1, 2, 3))`              |
| Python 集合      | `np.array(list(set))`           | `np.array(list({1, 2, 3}))`        |
| Python 字典      | `np.array(list(dict.values()))` | `np.array(list({'a':1}.values()))` |
| PyTorch 张量     | `tensor.numpy()`                | `torch_tensor.numpy()`             |
| TensorFlow 张量  | `tensor.numpy()`                | `tf_tensor.numpy()`                |
| Pandas Series    | `series.to_numpy()`             | `pd_series.to_numpy()`             |
| Pandas DataFrame | `df.to_numpy()`                 | `df.to_numpy()`                    |
| SciPy 稀疏矩阵   | `sparse_matrix.toarray()`       | `csr_matrix.toarray()`             |
| 生成器           | `np.fromiter(gen, dtype)`       | `np.fromiter(gen, int)`            |
| 字符串           | `np.array(list(str))`           | `np.array(list("hello"))`          |
| PIL 图像         | `np.array(image)`               | `np.array(PIL_image)`              |

这些方法涵盖了大多数常见的数据类型转换场景。根据您的具体需求，选择合适的方法可以高效地将数据转换为 NumPy 数组。
