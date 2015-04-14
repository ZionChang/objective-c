
#NSDictionary

字典是在iOS开发中经常会用到的一种数据类型,其中包含key和value,是一种无序集合,需要注意几点

1. key不会进行重复
2. 键值成对出现
3. 其中不能设置为nil


* [初始化](#init)
* [取值](#value)
* [遍历](#traversal)

<span id = "init">
##初始化

```objc
NSDictionary *dic1 = [NSDictionary dictionaryWithObjectsAndKeys:@"zhangsan", @"name", @24, @"age",  nil];
// 初始化简写
NSDictionary *dic2 = @{@"name":@"lisi", @"age":@34};
```

<span id = "value">
##取值

```objc
// 取值操作
NSLog(@"%@", [dic1 objectForKey:@"age"]);
```

<span id = "traversal">
##遍历

```objc
for (id obj in dic1.allKeys) {
   NSLog(@"%@", [dic1 objectForKey:obj]);
   // 简写
   NSLog(@"%@", dic1[obj]);
}
```