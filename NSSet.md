#NSSet

NSSet同样是一个<font color = "red">无序</font>的集合,其次NSSet中不允许有相同的对象存在.

NSSet每次打印都是同样的数据,以及每次取值`anyObject`也是同样的数值,是因为NSSet采用Hash表（其实就是数组）来保存元素,但集合元素位于底层Hash表的位置对于开发者来说是透明的,因此,无论调用多少次该方法,返回的总是同一个集合元素

* [初始化](#init)
* [数量](#count)
* [查找](#contain)
* [判断](#equal)
* [获取对象](#object)
* [遍历](#traversal)

<span id = "init">
##初始化

```objc
NSSet *set = [NSSet setWithObjects:@"25",@"age",@"张三",@"name",@"男",nil];

NSSet *set1 = [NSSet setWithObjects:@"25",@"age",@"张三",@"name",@"男",@"性别",nil];

// 以数组进行初始化
NSArray *array = @[@"hello", @"world", @"ios"];
NSSet *set2 = [NSSet setWithArray:array];

```
<span id = "count">
##数量

```objc
NSLog(@"set count:%lu", [set count]);
```
<span id = "contain">
##查找

```objc
//判断是否含有age字符串
if([set containsObject:@"age"]) {
   NSLog(@"set包含age");
}
```

<span id = "equal">
##判断

```objc
//判断set 是否等于set1
if ([set isEqualToSet:set1]) {
   NSLog(@"set 等于 set1");
}
//判断set 是否是set1的子集合
if ([set isSubsetOfSet:set1]) {
  	NSLog(@"set isSubsetOfSet set1");
}
```

<span id = "object">
##获取对象

```objc
//获取所有set对象
NSArray *array = [set allObjects];
NSLog(@"array:%@", array);
// 取出任意对象
id obj = [set anyObject];
NSLog(@"%@", obj);
```

<span id = "traversal">
##遍历

```objc
//迭代遍历
NSEnumerator *enumerator = [set objectEnumerator];
for (NSObject *object in enumerator) {
   NSLog(@"set1里的对象:%@", object);
}
```
