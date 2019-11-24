# 用Pythonic方式思考

### Item3: Know the difference between `bytes, str, unicode`
+ python3中, bytes实例包含原始的8位值, str包含Unicode字符;
+ python2中, str实例包含原始的8位值, unicode包含Unicode字符;
+ 把Unicode字符表示为二进制数据，最常见的编码方式是UTF-8
+ python3中，接受`str,bytes`，总是返回`str`的方法
```python
def to_str(bytes_or_str):
    if isinstance(bytes_or_str, bytes):
        value = bytes_or_str.decode('utf-8')
    else:
        value = bytes_or_str
    return value # Instance of str
```
+ python3中，接受`str,bytes`,总是返回`bytes`的方法
```python
def to_bytes(bytes_or_str):
    if isinstance(bytes_or_str, str):
        value = bytes_or_str.encode('utf-8')
    else:
        value = bytes_or_str
    return value # Instance of bytes
```
+ python3默认以UTF-8打开文件;python2默认以二进制打开文件


### Item16: 考虑用生成器来改写直接返回列表的函数
```python
### 旧写法：
def index_words(text):
  result = []
  if text:
    result.append(0)
  for index, letter in enumerate(text):
    if letter == ' ':
      result.append(index + 1)
  return result
### 新写法：
def index_words_iter(text):
  if text:
    yield 0
  for index, letter in enumerate(text):
    if letter == ' ':
      yield index + 1
result = list(index_words_iter(address))
```



### Item21: 用只能以关键字形式指定的参数来确保代码明晰
+ 下面的*后面的参数必须以关键字形式调用
```python
def safe_division_c(number, divisor, *, ignore_overflow=False,
                    ignore_zero_division=False):
    #### something
safe_division_c(1, 10**500, True, False) # Error
safe_division_c(1, 0, ignore_zero_division=True) # OK
```






