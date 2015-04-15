
# 数组


数组只能存储<font color = "red">对象类型</font>,并且结束标示符为nil,所以尤为注意，所以需要存储空类型，需要使用NSNull.

* [初始化](#init)
* [取值](#get)
* [获取数量](#count)
* [查询](#contain)
* [增加](#add)
* [切分数组](#join)
* [排序](#sort)
* [遍历](#traversal)


<span id = "init">
##初始化

常用初始化方法列表

```objc
+ (instancetype)array;
+ (instancetype)arrayWithObject:(id)anObject;
+ (instancetype)arrayWithObjects:(id)firstObj, ... NS_REQUIRES_NIL_TERMINATION;
+ (instancetype)arrayWithArray:(NSArray *)array;
+ (NSArray *)arrayWithContentsOfFile:(NSString *)path;
+ (NSArray *)arrayWithContentsOfURL:(NSURL *)url;
```

示例:

```objc
// 初始化方法
NSArray *array1 = [NSArray arrayWithObjects:@"hello", @"world", @"iOS", @"android", nil];
// 简写:
NSArray *array2 = @[@"hello", @"world"];
```

<span id = "get">
##取值

这里有id的详细说明[id和instancetype区别](http://archerzz.ninja/ios/id-instancetype.html)

```objc
// 取值
id object1 = [array1 objectAtIndex:2];
// 简写
id object2 = array1[2];
// 取下标
NSUInteger index = [array indexOfObject:@"iOS"]

```

<span id = "count">
##获取数量

```objc
// 计数
NSLog(@"count = %ld", array1.count);
```

<span id = "contain">
##查询

```objc
// 查询
NSLog(@"%d", [array1 containsObject:@"123"]);
```

<span id = "add">
##增加

```objc
// 增加一个元素
NSArray *array3 = [array1 arrayByAddingObject:@"123"];
// 增加一个数组所有的元素
NSArray *array4 = [array1 arrayByAddingObjectsFromArray:array2];
NSLog(@"array3 = %@", array3);
NSLog(@"array4 = %@", array4);
```

<span id = "join">
##切分数组

```objc
NSArray *array = @[@"www", @"baidu", @"com"];
// 利用点拼接数组元素
NSString *string = [array componentsJoinedByString:@"."];
// 利用点分割字符串
NSArray *newArray = [string componentsSeparatedByString:@"."];
```

<span id = "sort">
##排序

```objc
NSArray *array = [NSArray arrayWithObjects:@"hello", @"world", @"iOS", @"android", nil];
```

###使用系统方法

<font color = "red">默认是升序</font>

```objc
// 区分大小写排序
NSArray *sortedArray = [array sortedArrayUsingSelector:@selector(compare:)];
// 不区分大小写排序
NSArray *sortedArray1 = [array sortedArrayUsingSelector:@selector(caseInsensitiveCompare:)];

```

###使用代码块

```objc
// 使用代码块
NSArray *sortedArray2 = [array1 sortedArrayUsingComparator:^NSComparisonResult(id obj1, id obj2) {
   // 主要逻辑，决定当前是升序还是降序
   // 如果在return之后加上负号，则降序。
   return [obj1 compare:obj2];
}];  
```



<span id = "traversal">
##遍历数组

```objc
// 第一种
for (int i = 0; i < array.count; i ++) {
   NSLog(@"%@", array[i]);
}
// 快速遍历
for (id obj in array) {
   NSLog(@"%@", obj);
}
// 使用枚举器
NSEnumerator *enumerator = [array objectEnumerator];
id obj = [enumerator nextObject];
while (obj) {
   NSLog(@"枚举%@", obj);
   obj = [enumerator nextObject];
}

```

