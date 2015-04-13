# 日期

直接获取的日期都是<font color = "red">格林尼治时间</font>,所以我们获取的时间要少8个小时,如果要获取当前时间,需要用到NSTimeZone,我们待会统一讲解.

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

##获取秒数



##比较

##NSDateFormatter

