
我们有时为了数据存储方便，我们希望将一些自定义数据类型(结构体、共用体等)封装成对象，那么此时我们就会用到`NSValue`

* [系统结构体](#system)
	* [封装](#system-encapsulation)
	* [解封装](#system-decapsulation)
* [自定义结构体](#custom)
	* [封装](#custom-encapsulation)
	* [解封装](#custom-decapsulation)


<span id = "system">
##系统结构体

常用方法列表

```objc

// 封装
+ (NSValue *)valueWithRange:(NSRange)range;
+ (NSValue *)valueWithPoint:(NSPoint)point;
+ (NSValue *)valueWithSize:(NSSize)size;
+ (NSValue *)valueWithRect:(NSRect)rect;
// 只能系统10.10或者iOS8.0以上才能使用
+ (NSValue *)valueWithEdgeInsets:(NSEdgeInsets)insets NS_AVAILABLE(10_10, 8_0);

// 获取
@property (readonly) NSPoint pointValue;
@property (readonly) NSSize sizeValue;
@property (readonly) NSRect rectValue;
@property (readonly) NSEdgeInsets edgeInsetsValue NS_AVAILABLE(10_10, 8_0);

```
<span id = "system-encapsulation">

###封装
示例: 封装系统的相对来说比较简单

```objc
NSValue *value = [NSValue valueWithPoint:CGPointMake(10, 10)];
NSLog(@"%@", value);
// 打印结果
2015-04-13 20:21:12.024 OC_Lesson3[669:28657] NSPoint: {10, 10}
```

<span id = "system-decapsulation">
###解封装

解封装就比较简单了，只需要在上面的基础上:

```objc
CGPoint point = [value pointValue];
```


<span id = "custom">

常用方法列表

```objc
// 封装
// 参数1：需要存储的结构体指针
// 参数2：使用@encode()关键字，进行转换
+ (NSValue *)valueWithBytes:(const void *)value objCType:(const char *)type;

// 解封装
// 参数1：需要接受的结构体指针
- (void)getValue:(void *)value;

```

##自定义结构体
<span id = "custom-encapsulation">
###封装

```objc
Student stu = {"zhangsan", 78};
NSValue *value = [NSValue valueWithBytes:&stu objCType:@encode(Student)];
NSLog(@"%@", value);
```

<span id = "custom-decapsulation">
###解封装

```objc
Student newStu;
[value getValue:&newStu];
NSLog(@"name = %s, score = %.2f", newStu.name, newStu.score);
```
