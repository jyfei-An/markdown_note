# 导入

```python
import pandas as pd
```

# 数据类型的算术运算

| 方法             | 说明                     |
| ---------------- | ------------------------ |
| .add(d, **argws) | 类型间加法运算，可选参数 |
| .sub(d, **argws) | 类型间减法运算，可选参数 |
| .mul(d, **argws) | 类型间乘法运算，可选参数 |
| .div(d, **argws) | 类型间除法运算，可选参数 |

```python
#创建3行4列的矩阵
m1 = pd.DataFrame(np.arange(12).reshape(3, 4))
print(m1)
#创建4行5列的矩阵
n1 = pd.DataFrame(np.arange(20).reshape(4, 5))
print(n1)

#算术运算根据行列索引，补齐后运算，运算默认产生浮点数，
#每行每列对应元素相加，维度不一样使用100填充
n1.add(m1, fill_value = 100)
#每行每列对应元素相乘，维度不一样使用100填充
n1.mul(m1, fill_value = 0)
```

基本统计分析函数

![image-20210114222604582](https://i.loli.net/2021/01/14/xuLWRhFIU9faZ1g.png)

