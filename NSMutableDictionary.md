#可变字典

NSMutableDictionary继承与NSDictionary,所以同样拥有父类的所有方法

初始化一个字典

```objc
NSDictionary *dic1 = [NSDictionary dictionaryWithObjectsAndKeys:@"zhangsan", @"name", @24, @"age",  nil];
```


##增加更新

```objc
// 当key存在的时候，就相当于修改操作
// 当key不存在的时候，就相当于增加操作
// 增加
[dic2 setObject:@1.82 forKey:@"height"];
// 更新
[dic2 setObject:@"lisi" forKey:@"name"];
```


##删除

```objc
 // 根据key删除某一个键值对
[dic2 removeObjectForKey:@"age"];
// 删除所有
[dic2 removeAllObjects];
```

