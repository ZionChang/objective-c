# 日期

直接获取的日期都是<font color = "red">格林尼治时间</font>,所以我们获取的时间要少8个小时,如果要获取当前时间,需要用到NSTimeZone,我们待会统一讲解.

* [初始化](#init)
* [获取秒数](#seconds)
* [比较](#compare)
* [NSDateFormatter](#formatter)


<span id = "init">
##初始化

```objc
// 获取当前时间
NSDate *date = [NSDate date];
// 获取1970年10秒后的时间
NSDate *date1 = [NSDate dateWithTimeIntervalSince1970:10];
// 获取现在20秒后的时间
NSDate *date2 = [NSDate dateWithTimeIntervalSinceNow:20];
// 获取从date开始的20秒后的时间
NSDate *date3 = [NSDate dateWithTimeInterval:20 sinceDate:date];
```
<span id = "seconds">
##获取秒数

```objc
// NSTimerInterval 等价于 double
NSTimeInterval timeInterval = [date timeIntervalSince1970];
```
<span id = "compare">
##比较

方法列表

```objc
- (NSDate *)earlierDate:(NSDate *)anotherDate;
- (NSDate *)laterDate:(NSDate *)anotherDate;
- (NSComparisonResult)compare:(NSDate *)other;
- (BOOL)isEqualToDate:(NSDate *)otherDate;
```

示例:

```objc
NSDate *date = [NSDate date];
NSDate *date1 = [NSDate dateWithTimeIntervalSince1970:10];
    
NSDate *earlierDate = [date earlierDate:date1];
NSDate *laterDate = [date1 laterDate:date1];
    
NSComparisonResult result = [date compare:date1];
if (result == NSOrderedAscending) {
   NSLog(@"升序");
} else if (result == NSOrderedSame) {
   NSLog(@"相同");
} else {
   NSLog(@"降序");
}
    
if ([date isEqualToDate:date1]) {
   NSLog(@"相同");
} else {
   NSLog(@"不同");
}

    

```
<span id = "formatter">
##NSDateFormatter

示例:

```objc
NSDate *date = [NSDate date];
   
NSDateFormatter *formatter = [[NSDateFormatter alloc] init];
// 使用系统格式化
[formatter setTimeStyle:NSDateFormatterFullStyle];
[formatter setDateStyle:NSDateFormatterFullStyle];
    
NSString *string = [formatter stringFromDate:date];
    
NSLog(@"string = %@", string);

```

打印结果:

```objc

2015-04-13 21:52:09.471 OC_Lesson3[1217:78328] string = 2015-04-13 01:52:09
```

同样我们也可以<font color = "red">自定义样式</font>:

<font color = "red">自定义样式</font>可以查看[http://archerzz.ninja/ios/formatter-character.html](http://archerzz.ninja/ios/formatter-character.html)

```objc

NSDate *date = [NSDate date];
   
NSDateFormatter *formatter = [[NSDateFormatter alloc] init];
// 自定义样式    
[formatter setDateFormat:@"yyyy-MM-dd HH:mm:ss"];
    
NSString *string = [formatter stringFromDate:date];
    
NSLog(@"string = %@", string);
```

打印结果:

```objc
2015-04-13 21:54:43.036 OC_Lesson3[1233:79562] string = 2015-04-13 21:54:43
```