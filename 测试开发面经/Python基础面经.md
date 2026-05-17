### 1、给一个列表去重，并且相对位置保持不变？
利用SET集合
```python
list=[1,2,2,2,3,3,4,5]
new_list=list(set(list))
```
利用for循环
```python
list=[1,2,2,2,3,3,4,5]
b=[]
for item in list:
	if item not in b:
		b.append(item)
```

### 2、lambda 函数一般用在哪些场景？
Lambda函数，也称为匿名函数，它允许定义一个简单的、通常是单行的函数，而无需给函数命名。
lambda 参数列表: 表达式
λ函数的一些常见用法包括：
1. 将λ函数赋值给一个变量，通过变量间接调用该λ函数，例如：
    `add = lambda x, y: x + y`  
    `print(add(3, 4))`
2. 将λ函数赋值给其他函数，从而替换原有函数的功能，例如：
    `sum = lambda *args: None`
3. 将λ函数作为参数传递给其他函数，例如与`map()`函数结合使用，对序列中的每个元素应用函数进行映射操作：
    `numbers = (1, 2, 3, 4, 5)`  
    `result = list(map(lambda x: x ** 3, numbers))`
4. 与`sorted()`函数结合使用，指定排序的依据，例如按照列表中元素的某个属性进行排序：
    `students = [{'name': 'tom', 'age': 20}, {'name': 'rose', 'age': 19}, {'name': 'jack', 'age': 22}]`  
    `# 按 name 值升序排列`  
    `students.sort(key=lambda x: x['name'])`

### 4、Python的垃圾回收机制
这是一种自动的内存管理机制。当Python中的对象没有任何变量引用它时，这个对象就变为垃圾。Python的垃圾收集器会定期运行，并清除这些垃圾。
```python
# 创建一个对象
my_object = SomeObject()
# 当my_object变量被重新赋值时，原来的对象就没有任何引用了
my_object = None
# 此时，原来的对象就成为垃圾，等待垃圾收集器回收
```
### 5、numpy和pandas库常用的函数有哪些，进行数据查找的函数
**NumPy 常用函数：**
1. `np.array()`：创建数组。
2. `np.zeros()`：创建全零数组。
3. `np.ones()`：创建全一数组。
4. `np.arange()`：创建一个数值序列的数组。
5. `np.linspace()`：创建在指定范围内等间隔分布的数组。
6. `np.reshape()`：改变数组的形状。
7. `np.dot()`：矩阵乘法。
**Pandas 常用函数：**
1. `pd.read_csv()`：读取 CSV 文件。
2. `pd.DataFrame()`：创建数据框。
3. `df.head()`：查看数据框的前几行。
4. `df.tail()`：查看数据框的后几行。
5. `df.info()`：获取数据框的基本信息。
6. `df.describe()`：获取数据框的描述性统计信息。
在数据查找方面：
**NumPy**：  
可以使用条件索引来查找满足特定条件的元素，例如：`arr[arr > 5]` 查找数组 `arr` 中大于 5 的元素。
**Pandas**：
3. `query` 方法通过表达式进行查找：
```
found_rows = df.query('A > 1')
```
### 6、`is` 和 `==`的区别
`is` 用于比较两个对象是否是同一个对象（即它们的内存地址是否相同）
`==` 比较的是值是否相等，对象不同

### 7、pandas库中apply和apply(lambda)区别
apply和apply(lambda)都用于对逐行和逐列的操作
apply可以接受一个函数作为参数
```python
import pandas as pd
df=pd.DataFrame({'column_A':[1,2,3]})
def double_value(num):
	return num**2
result=df['A'].apply(double_value)
```
apply(lambda)则是在apply中使用匿名函数lambda
```python
import pandas as pd
df=pd.DataFrame({'column_A':[1,2,3]})
result=df['A'].apply(lambda x:x**2)
```

### 8、Python装饰器作用？原理？
在修改装饰函数源代码和调用方式的前提下，为函数添加额外功能
**原理**：@decorator函数可以修饰func函数
1、在@decorator装饰器函数下 ，定义wrapper函数，这个函数会包含一些逻辑，并且会调用func函数
2、decorator函数会返回wrapper函数
3、解释器在遇到@decorator函数装饰func，会将func返回给decorator，然后将func重新绑定到decorator返回的wrapper函数
```python
import time

#定义一个日志记录功能，记录函数运行的时间和输入参数
def log_function_call(func):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        print(f"Calling {func.__name__} with args: {args}, kwargs: {kwargs}")
        result = func(*args, **kwargs)
        end_time = time.time()
        print(f"{func.__name__} completed in {end_time - start_time} seconds")
        return result
    return wrapper

@log_function_call
def add_numbers(a, b):
    return a + b
```


### Python执行Linux命令，查找某个文件夹下包含Python的文件，并打印出文件名和路径？
使用`os.system()`函数执行单个命令，例如os.system('ls -l')

```python
import os

folder_path = '/your/specific/folder/path'  # 将这里替换为实际的文件夹路径
for root, dirs, files in os.walk(folder_path):
    for file_name in files:
        file_path = os.path.join(root, file_name)
        try:
            with open(file_path, 'r', encoding='utf-8') as f:
                content = f.read()
                if 'Python' in content:
                    print(f'文件名：{file_name}, 路径：{file_path}')
        except Exception as e:
            pass
```

### Python正则表达式re，怎么使用？
```python
import re
text='hello world'
match=re.match(r'hello',text)
print(match)
search=re.search(r'world',text)
print(search)
all_matches=re.findall(r'o',text)
print(all_matches)
```

### 常用的命令
```python
string.lower()将字母变成小写
string.upper()将字母变成小写
string.isalpha()判断字符是否是字母
```

### 生成元素的组合和排列
```python
import itertool
iterable = [1, 2, 3] 
r = 2
#生成可迭代对象中元素的 `r` 个元素的组合，组合不考虑元素顺序
combinations=itertool.combinations(iterable,r)
#生成可迭代对象中元素的 `r` 个元素的排列，排列考虑元素顺序
permutations=itertool.permutations(iterable,r)
```

### 格式化字符串
**f-string**
```python
item='basketball'
s=12
print(f'the amount of {item} is {s:.2f} RMB)
```
### 列表生成表达式
```python
list=[1,2,3,4,5,6,7,8]
list1=[i**2 for i in list if i %2 == 0]
```

### `func(*args, **kw)`两个参数的区别
`*args`是用来接收任意数量的位置参数，参数收集在元组中
`**kw`用于接收任意数量的关键字参数，参数收集在字典中
```python
def my_func(*args, **kw):
    print("Positional arguments:", args)
    print("Keyword arguments:", kw)

my_func(1, 2, 3, a=4, b=5)
```

### 深拷贝和浅拷贝
浅拷贝会创建一个新的对象，但这个新对象中的某些元素（如果是复合对象，比如列表嵌套列表、字典嵌套字典等情况）可能仍然指向与原始对象相同的内存地址。
深拷贝会创建一个全新的对象，并且该对象及其所有子对象（无论是简单对象还是复合对象）都与原始对象完全独立，它们占据不同的内存空间。