大家在使用的过程一定注意一点，不要<font color = "red">越界</font>

并且NSMutableString使用的修改字符串的方法，都是在改变自己本身，大家可以注意到都没有<font color = "red">返回值</font>，这就是和NSString的区别

但是NSString是其父类，意味着NSMutableString的对象也可以调用父类的所有的公开方法。

* [初始化](#init)
* [插入](#insert)
* [删除](#delete)
* [追加](#append)
* [替换](#replace)

<span id = "init">
##初始化

```objc
// 采用父类的方法进行初始化
NSMutableString *string = [NSMutableString stringWithFormat:@"hello world!"];
```
<span id = "insert">
##插入



```objc
[string insertString:@"my" atIndex:5];
```

<span id = "delete">
##删除

```objc
// 从第1个开始，删除2个
[string deleteCharactersInRange:NSMakeRange(1, 2)];

```

<span id = "append">
##追加


```objc
// 以格式化方式追加
[string appendFormat:@"count = %d", 5];
// 直接字符串追加
[string appendString:@"hello"];
```

<span id = "replace">
##替换

```objc
// 在一个范围内进行替换
[string replaceCharactersInRange:NSMakeRange(1, 10) withString:@""];

```
