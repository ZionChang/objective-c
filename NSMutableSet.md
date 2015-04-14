#NSMutableSet

首先我们来初始化两个set

```objc
NSMutableSet *muSet = [NSMutableSet set];
NSSet *set = [NSSet setWithObjects:@"hello",@"world",@"ios", nil];

```

##增加

```objc
[muSet addObject:@"hello"];
```

##合并

```objc
[muSet unionSet:set];
```
##截取

```objc
[muSet addObject:@"asdf"];
// 此时 由于muSet中@"asdf"在set中不存在,所以自动删除
[muSet intersectSet:set];
```

##删除

```objc
NSSet *set1 = [NSSet setWithObjects:@"world",@"ios", nil];
[muSet minusSet:set1];
```

