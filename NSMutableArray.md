#NSMutableArray

可变数组,主要方便我们进行增删改查,继承与NSArray

* [初始化](#init)
* [增加](#add)
* [插入](#insert)
* [修改](#modify)
* [删除](#remove)
* [查找](#contain)
* [交换](#exchange)
* [排序](#sort)

<span id = "init">
##初始化

初始化方式直接使用父类的初始化方式

```objc
NSMutableArray *array = [[NSMutableArray alloc] initWithObjects:@"hello", @"world", nil];
```

<span id = "add">
##增加

```objc
// 增加到最后
[array addObject:@"android"];
```

<span id = "insert">
##插入

```objc
[array insertObject:@"iOS" atIndex:1];
```

<span id = "modify">
##修改

```objc
// 将下标为2的对象以后面传入的对象进行替换
[array replaceObjectAtIndex:2 withObject:@"iOS!!!!"];
```
<span id = "remove">
##删除

```objc
// 删除具体某一个
[array removeObjectAtIndex:0];
// 以范围进行删除,从第1个开始，删除2个
[array removeObjectsInRange:NSMakeRange(1, 2)];
// 删除所有元素
[array removeAllObjects];
// 删除最后一个
[array removeLastObject];

```

<span id = "contain">
##查找

直接使用父类的方法

```objc
[array containsObject:@"android"];
```

<span id = "exchange">
##交换

```objc
// 下标为1的对象与下标为2的对象进行交换
[array exchangeObjectAtIndex:1 withObjectAtIndex:2];
```

<span id = "sort">
##排序

```objc
// 使用系统方式
[array sortUsingSelector:@selector(caseInsensitiveCompare:)];
// 使用代码块
[array sortUsingComparator:^NSComparisonResult(id obj1, id obj2) {
   return [obj1 compare:obj2];
}];

```