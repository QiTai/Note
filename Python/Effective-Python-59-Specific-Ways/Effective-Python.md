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


