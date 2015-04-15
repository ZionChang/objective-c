#NSCalendar

* [初始化](#init)
* [设置工作日](#work)
* [设置区域](#area)
* [设置时区](#time)
* [获取日历信息](#calendar)
* [NSDateComponents](#components)
* [获取时间组件](#getComponents)
* [创建日期](#create)
* [根据身份证获取年龄](#code)

<span id = "init">
##初始化


###获取本地信息

```objc
//+ currentCalendar
//取得当前用户的逻辑日历
//currentCalendar取得的值会一直保持在cache中,第一次取得以后如果用户修改该系统日历设定，这个值也不会改变。
NSCalendar *calendar = [NSCalendar currentCalendar];
NSLog(@"calendar = %@",calendar);

//+ (id)autoupdatingCurrentCalendar
//取得当前用户的逻辑日历
//用autoupdatingCurrentCalendar，那么每次取得的值都会是当前系统设置的日历的值。
NSCalendar *autoupdatingCurrent = [NSCalendar autoupdatingCurrentCalendar];
NSLog(@"autoupdatingCurrent = %@",autoupdatingCurrent);
```

###自定义日历

```objc
/*
iOS8都被替换成其他的字符串，点进头文件就可以看见
FOUNDATION_EXPORT NSString * const NSGregorianCalendar;        //公历（常用）
FOUNDATION_EXPORT NSString * const NSBuddhistCalendar;         //佛教日历
FOUNDATION_EXPORT NSString * const NSChineseCalendar;          //中国农历（常用）
FOUNDATION_EXPORT NSString * const NSHebrewCalendar;           //希伯来日历
FOUNDATION_EXPORT NSString * const NSIslamicCalendar;          //伊斯兰历
FOUNDATION_EXPORT NSString * const NSIslamicCivilCalendar;     //伊斯兰教日历
FOUNDATION_EXPORT NSString * const NSJapaneseCalendar;         //日本日历(和历，常用)
FOUNDATION_EXPORT NSString * const NSRepublicOfChinaCalendar;  //中华民国日历（台湾）
FOUNDATION_EXPORT NSString * const NSPersianCalendar;          //波斯历
FOUNDATION_EXPORT NSString * const NSIndianCalendar;           //印度日历
FOUNDATION_EXPORT NSString * const NSISO8601Calendar;          //ISO8601（但是现在还不可用）
*/

初始化的时候ident就传入以上数据的一种

- (id)initWithCalendarIdentifier:(NSString *)ident NS_DESIGNATED_INITIALIZER;
```

举例:

```objc
 NSCalendar *initCalendar = [[NSCalendar alloc]initWithCalendarIdentifier:NSCalendarIdentifierGregorian];
        NSLog(@"%@", initCalendar);
```

<span id = "work">
##设置工作日

```objc
//- setFirstWeekday:
//设置第一个工作日
//设定每周的第一天从星期几开始，比如:
//.  如需设定从星期日开始，则value传入1
//.  如需设定从星期一开始，则value传入2
//.  以此类推
[initCalendar setFirstWeekday:1];
```

<span id = "area">
##设置区域

```objc
[initCalendar setLocale:[[NSLocale alloc] initWithLocaleIdentifier:@"en_US"]];
//设定作为(每年及每月)第一周必须包含的最少天数，比如:. 如需设定第一周最少包括7天，则value传入7
//– setMinimumDaysInFirstWeek:
[initCalendar setMinimumDaysInFirstWeek:7];
```
<span id = "time">
##设置时区

```objc
[initCalendar setTimeZone:[NSTimeZone defaultTimeZone]];
```
<span id = "calendar">
##获取日历信息

###日历标示符

```objc
//返回日历标示符
NSString *calendarIdentifier = [initCalendar calendarIdentifier];
NSLog(@"calendarIdentifier = %@",calendarIdentifier);
```

###获取每周的第一天

```objc
//– firstWeekday
//返回日历指定的每周的第一天从星期几开始。缺省为星期天，即firstWeekday = 1

NSUInteger firstWeekday = [initCalendar firstWeekday];
NSLog(@"firstWeekday = %lu",firstWeekday);
```

###返回日历指定的地区信息

```objc
NSLocale *locale = [initCalendar locale];
NSLog(@"locale = %@",locale.localeIdentifier);
```

###获取范围

```objc
//– maximumRangeOfUnit:    //返回单元的最大范围
//- minimumRangeOfUnit:    //返回单元的最小范围 //比如Day Calendar Unit就是一个月最多31天这个意思
NSRange range = [initCalendar maximumRangeOfUnit:NSCalendarUnitDay];
NSLog(@"range = %lu",range.length);
//- minimumDaysInFirstWeek
//返回日历指定的第一周必须包含的最少天数。
NSUInteger minimumDays = [initCalendar minimumDaysInFirstWeek];
NSLog(@"minimumDays = %lu",minimumDays);
```

<span id = "components">
##NSDateComponents

获取时间组件

```objc
NSDateComponents *dc = [[NSDateComponents alloc] init];
[dc setYear: 2013];
[dc setMonth: 4];
[dc setDay: 6];
////
NSDate *date = [calendar dateFromComponents:dc];

```
<span id = "getComponents">
##获取时间组件

```objc
//返回时间组件

// 利用逻辑非连接你想要的组件
unsigned unitFlags = NSCalendarUnitYear | NSCalendarUnitMonth |  NSCalendarUnitDay;
// 获取相应的组件
NSDateComponents *comps = [initCalendar components:unitFlags fromDate:[NSDate date]];
NSLog(@"NSDateComponents - %lu",comps.year);

//- components:fromDate:toDate:options:
//返回时间组件 比较2个日期
NSDate *startDate = date;
NSDate *endDate = [NSDate date];

unsigned int unitFlags2 = NSCalendarUnitMonth | NSCalendarUnitDay;
NSDateComponents *comps2 = [initCalendar components:unitFlags2 fromDate:startDate  toDate:endDate  options:0];
NSInteger months = [comps2 month];
NSInteger days = [comps2 day];
NSLog(@"months = %ld days = %ld", months, days);
```
<span id = "create">
##创建日期

```objc
NSCalendar *calendar = [NSCalendar currentCalendar];
NSDateComponents *comps = [[NSDateComponents alloc] init];
[comps setYear:1965];
[comps setMonth:1];
[comps setDay:1];
[comps setHour:2];
[comps setMinute:10];
[comps setSecond:0];
NSDate *date = [calendar dateFromComponents:comps];
NSLog(@"date = %@",date);

```

<span id = "code">
##通过身份证获取年龄姓名

创建一个Person类,如下:

```objc
#define Code_Number 18      // 身份证号码个数
#define Sex_Start 16        // 性别起始位置
#define Sex_Length 1        // 性别长度
#define Birthday_Start 6    // 出生日期起始位置
#define Birthday_Length 8   // 出生日期长度

@interface Person : NSObject
{
    NSString * _name;           // 姓名
    NSString * _code;           // 身份证号
    NSString * _sex;            // 性别
    NSString * _birthday;       // 出生日期
    NSInteger _age;             // 年龄
}

- (instancetype)initWithCode:(NSString *)code;
```

在.m文件中实现相应的根据身份证获取年龄性别等


```objc
- (instancetype)initWithCode:(NSString *)code
{
    if (self = [super init]) {
    // 判断身份证合法
        if (code.length == Code_Number) {
            _code = code;

            // 获取sex的字符串，并且判断是单数还是双数
            NSString * codeString = [_code substringWithRange:NSMakeRange(Sex_Start, Sex_Length)];
            if ([codeString integerValue] % 2) {
                _sex = @"男";
            } else {
                _sex = @"女";
            }
            // 获取出生日期的字符串
            _birthday = [_code substringWithRange:NSMakeRange(Birthday_Start, Birthday_Length)];
            // 设置相对应的格式
            NSDateFormatter * formatter = [[NSDateFormatter alloc] init];
            // 必须和字符串的格式相匹配
            [formatter setDateFormat:@"yyyyMMdd"];
            // 获取出生日期
            NSDate * birthdayDate = [formatter dateFromString:_birthday];
            NSLog(@"%@", birthdayDate);
            // 获取现在日期
            NSDate * nowDate = [NSDate date];
            // 初始化一个日历(用中国的一个字符串作为标示）
            NSCalendar * calendar = [[NSCalendar alloc] initWithCalendarIdentifier:NSCalendarIdentifierRepublicOfChina];
            // 设置所需要的枚举，我们这里需要的年
            NSCalendarUnit unit = NSCalendarUnitYear | NSCalendarUnitMonth | NSCalendarUnitDay;
            // 算出出生日期到现在相差的年数 来获取年龄
            NSDateComponents * dateComponents = [calendar components:unit fromDate:birthdayDate toDate:nowDate options:NSCalendarWrapComponents];
            _age = [dateComponents year];
        }
    }
    return self;
}

```
