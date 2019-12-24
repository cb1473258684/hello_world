# Pands社区
陈贝 51195100002 作业

## 1.pandas概述:

pandas是python的核心数据分析支持库，提供了快速、灵活、明确的数据结构，旨在简单、直观地处理关系型、标记型数据。Pandas 的目标是成为 Python 数据分析实践与实战的必备高级工具，其长远目标是成为最强大、最灵活、可以支持任何语言的开源数据分析工具。经过多年不懈的努力，Pandas 离这个目标已经越来越近了。

Pandas 适用于处理以下类型的数据：

- 与 SQL 或 Excel 表类似的，含异构列的表格数据;
- 有序和无序（非固定频率）的时间序列数据;
- 带行列标签的矩阵数据，包括同构或异构型数据;
- 任意其它形式的观测、统计数据集, 数据转入 Pandas 数据结构时不必事先标记。

Pandas 的主要数据结构是 Series（一维数据）与 DataFrame（二维数据），这两种数据结构足以处理金融、统计、社会科学、工程等领域里的大多数典型用例。对于 R 用户，DataFrame 提供了比 R 语言 data.frame 更丰富的功能。Pandas 基于 NumPy 开发，可以与其它第三方科学计算支持库完美集成。

说明：

- Pandas 速度很快。Pandas 的很多底层算法都用 Cython 优化过。然而，为了保持通用性，必然要牺牲一些性能，如果专注某一功能，完全可以开发出比 Pandas 更快的专用工具。
- Pandas 是 statsmodels 的依赖项，因此，Pandas 也是 Python 中统计计算生态系统的重要组成部分。
- Pandas 已广泛应用于金融领域

数据结构

| 维数 | 名称      | 描述                               |
| ---- | --------- | ---------------------------------- |
| 1    | Series    | 带标签的一维同构数组               |
| 2    | DataFrame | 带标签的，大小可变的，二维异构表格 |

Pandas 数据结构就像是低维数据的容器。比如，DataFrame 是 Series 的容器，Series 则是标量的容器。使用这种方式，可以在容器中以字典的形式插入或删除对象。

------

## 2.pandas常用操作

### **一. DataFrame的创建**

创建一个空的dataframe 

```python
df=pd.DataFrame(columns={"a"``:``""``,``"b"``:``""``,``"c"``:``""``},index=[0])
```

```
   ``a  c  b``0` `NaN NaN NaN
```

用list的数据创建dataframe：

```python
a ``=` `[[``'2'``, ``'1.2'``, ``'4.2'``], [``'0'``, ``'10'``, ``'0.3'``], [``'1'``, ``'5'``, ``'0'``]]``df ``=` `pd.DataFrame(a, columns``=``[``'one'``, ``'two'``, ``'three'``])``print` `df
```

```python
 ``one two three``0`  `2` `1.2`  `4.2``1`  `0`  `10`  `0.3``2`  `1`  `5`   `0
```

用numpy的矩阵创建dataframe

```python
array ``=` `np.random.rand(``5``,``3``)
df=pd.DataFrame(array,columns``=``[``'first'``,``'second'``,``'third'``])
```

用dict的数据创建DataFrame

```python
data ``=` `{ ``'row1'` `: [``1``,``2``,``3``,``4``], ``'row2'` `: [``'a'` `, ``'b'` `, ``'c'` `, ``'d'``] }
df=pd.DataFrame(data) 
```

```python
dict` `=` `{ ``'row1'` `: [``1``,``2``,``3``,``4``], ``'row2'` `: [``'a'` `, ``'b'` `, ``'c'` `, ``'d'``] }``df ``=` `pd.DataFrame.from_dict(``dict``,orient``=``'index'``).T
```

读取csv或者excel文件为DataFrame格式

```python
df``=``pd.read_csv(``'D:/Program Files/example.csv'``)
```

excel一个表格中可能有多个sheet，sheetname可以进行选取

```python
df ``=` `df.read_excel(``'D:/Program Files/example.xls'``,sheetname``=``0``)
```



### 二. DataFrame的一些描述和类型**

 describe会显示dataframe的一些基本统计数据，数量、均值、中位数、标准差等

 head会显示dataframe的前几行，后几行：

```python
print` `df.describe()
print` `df.head()
print` `df.tail(``10``)
```

单独计算某列的统计值

```python
df[``'one'``].sum()
df[``'one'``].mean()
df[``'one'``].count()
df[``'one'``].max()
df[``'one'``].min()
```

查看dataframe的数据类型：

```python
print(df.dtypes)
```

查看dataframe的数据数目：

```python
print` `（df.size）
```

查看dataframe的形状：

```python
print` `(df.shape)
```

返回列数：

```python
print` `(df.ndim)
```

查看横纵坐标的标签名：

```python
print` `(df.axes)
```

　　

------

 

### **三. DataFrame的切片**

iloc索引或切片（iloc中只能取整数值）：

```python
print` `df.iloc[``1``,:] ``#第1行，所有列
print` `df.iloc[:,[``0``,``2``]] ``#第0行，第0列和第2列
print` `df[``'one'``].iloc[``2``] ``#列名索引+行号
```

loc索引或切片（loc中可以取str）：

```python
print` `data.loc[``0``:``1``, [``'one'``, three']]
```

筛选出dataframe中有某一个或某几个字符串的列：

```python
list=[``'key1'``,``'key2'``]``df = df[df[``'one'``].isin(list)]
```

筛选出dataframe中不含某一个或某几个字符串的列，相当于反选

```python
df ``=` `df[~df[``'one'``].isin(``list``)]
```

　　

------

###  **四. 缺失值的处理**

缺失值可以删除也可以用均值或者0等数填充：

```python
df.fillna(df1.mean())``df.fillna(``0``)
```

删除缺失值时可以指定列：

```python
df ``=` `df.dropna(subset``=``[``'one'``,``'two'``])
```

　　

### **五. 去重、删除行或列**

去重需要在subset指定哪一列的值进行筛选，如果不选择的话默认整行的值全部一样才去掉

first表示保留第一个出现的值所在行，last表示保留最后一个出现的重复值所在的行，false表示重复的行全部删除

```python
df``=``df.drop_duplicates(subset``=``'one'``,keep``=``'first'``)
```

去除有NaN值的行或列(axis=0去除行，=1去除列)：

```python
df ``=` `df.dropna(axis``=``0``)``df ``=` `df.dropna(axis``=``1``)
```

去除某一列：

```python
df ``=` `df.drop([``'one'``],axis``=``1``)
```

去除含有某一个数的行：

```python
row_list ``=` `df[df.one ``=``=` `2``].index.tolist() ``# 获得含有该值的行的行号``df ``=` `df.drop(row_list)
```



### 六. DataFrame的修改**

修改数据类型

```python
df[``'one'``]``=``pd.DataFrame(df[``'one'``],dtype``=``np.``float``)
```

修改列名（需要写上所有列名，包括需要修改的和不需要修改的）：

```python
df.columns ``=` `[``'first'``,``'second'``,``'all'``]
```

修改列名（只需写上需要修改的列）

```python
df.rename(columns ``=` `{``'one'``:``'first'``,``'two'``:``'second'``},inplace ``=` `True``) ``#inplace=True表示修改df，若为False表示只返回一个修改后的数据
```

重排序(by可以取多个列名,默认升序)：

```python
df ``=` `df.sort_values(by``=``[``'one'``],ascending ``=` `True``)
df ``=` `df.sort_index(axis ``=` `0``,ascending ``=` `True``,by ``=` `'one'``)
df ``=` `df.sort(columns ``=` `[``'one'``],axis ``=` `0``,ascending ``=` `True``)
```

修改数据

```python
df.iloc[``1``,``2``] ``=` `10
```

用已有的列进行运算创建新的列

```python
df[``'new_colume'``] ``=` `df[``'one'``] ``+` `df[``'two'``]
```

------

### **七. dataframe更改索引**

当删除掉不需要的行时，行索引会变的不连续，这时候可以重新设计新的索引

```python
df[``'index'``]``=``range``(``len``(df[``'one'``]))
df.set_index(``'index'``)
```

设置时间序列为索引

```python
dd ``=` `pd.date_range(start``=``'4/1/2018'``,periods``=``5``)``#dd = pd.date_range('4/1/2018','4/5/2018')``df ``=` `df.set_index(dd)
```

　　

------

###  **八. 添加新的行，将两个dataframe连接到一起**

axis表示连接的方向，axis=0表示两个dataframe的行数会增加，如果列名相同则直接共用列，如果列名不同会生成新的列；axis=1，表示会加上新的列

```python
df``=``pd.concat([df,df],axis``=``0``) ``# 连接后行数是以前的2倍，列数不变
```

在dataframe添加新的行

```python
df ``=` `df.append(df.loc[``2``,:],,ignore_index``=``True``)
```

如果两个dataframe的列名是一样的，也可以用merge：

```python
df ``=` `pd.merge(df,df)
```

------

### 九. DataFrame的输出

输出为excel或者csv格式,csv文件里的数据被读取时数据类型默认为object，excel则会保留原有的数据类型

```python
df.to_excel(``'path/filename.xls'``)``df.to_csv(``'path/filename.csv'``)
```

输出为numpy的矩阵格式

```python
matrix ``=` `df.ax_matrix()
```

输出为dict格式

```python
dict` `=` `df.to_dict(orient``=``"dict"``)
```

------

## 3.github上pandas开源作业

https://github.com/guipsamora/pandas_exercises

