
* [初始化](#init)
* [获取值](#value)
* [比较](#compare)
* [NSNumberFormatter](#formatter)
	* [设置格式](#style)
	* [类型转换](#change)

<span id = "init">
##初始化

NSNumber在初始化之后，只会获取<font color = "red">有效数据</font>，所以打印出来的3个数据都相同。

```objc

NSNumber *number1 = [NSNumber numberWithDouble:5.00];
NSNumber *number2 = [NSNumber numberWithFloat:5.0f];
NSNumber *number3 = [NSNumber numberWithInt:5];
NSLog(@"number1 = %@, number2 = %@, number3 = %@", number1, number2, number3);
// 打印结果
2015-04-13 19:48:47.262 OC_Lesson3[555:11811] number1 = 5, number2 = 5, number3 = 5

```
同样NSNumber可以进行简写的形式，类似于上面的便利构造方法

```objc
// 简写
NSNumber *number = @5;
// 如果以变量进行简写，只需要加上相应的括号
int count = 10;
NSNumber *newNumber = @(count);
```

<span id = "value">
##获取值

```objc
@property (readonly) char charValue;
@property (readonly) unsigned char unsignedCharValue;
@property (readonly) short shortValue;
@property (readonly) unsigned short unsignedShortValue;
@property (readonly) int intValue;
@property (readonly) unsigned int unsignedIntValue;
@property (readonly) long longValue;
@property (readonly) unsigned long unsignedLongValue;
@property (readonly) long long longLongValue;
@property (readonly) unsigned long long unsignedLongLongValue;
@property (readonly) float floatValue;
@property (readonly) double doubleValue;
@property (readonly) BOOL boolValue;
@property (readonly) NSInteger integerValue NS_AVAILABLE(10_5, 2_0);
@property (readonly) NSUInteger unsignedIntegerValue NS_AVAILABLE(10_5, 2_0);
@property (readonly, copy) NSString *stringValue;
```
通过以上属性就可以获取相应的基本数据，使用点语法，或者掉方法（getter方法）。

```objc
NSNumber *number = @5;
int value1 = [number intValue];
float value2 = [number floatValue];
```

<span id = "compare">
##比较

###地址比较

```objc
NSNumber *number1 = @1234;
NSNumber *number2 = @2345;

if (number1 == number2) {
   NSLog(@"地址相同");
} else {
   NSLog(@"地址不同")
}

```
###值比较


####compare

返回值为枚举类型

```objc

NSNumber *number1 = @1234;
NSNumber *number2 = @2345;
if ([number1 compare:number2] == NSOrderedSame) {
   NSLog(@"相同");
} else if ([number1 compare:number2] == NSOrderedAscending) {
   NSLog(@"升序");
} else {
   NSLog(@"降序");
}
```

####isEqualToNumber

返回值为BOOL类型

```objc

NSNumber *number1 = @1234;
NSNumber *number2 = @2345;
if ([number1 isEqualToNumber:number2]) {
   NSLog(@"值相同");
} else {
   NSLog(@"值不同");
}
```


<span id = "formatter">

##NSNumberFormatter

<span id = "style">
###设置格式

样式如下

```objc
typedef NS_ENUM(NSUInteger, NSNumberFormatterStyle) {
	 // 没有风格
    NSNumberFormatterNoStyle = kCFNumberFormatterNoStyle,
    // 12,345 这种样式
    NSNumberFormatterDecimalStyle = kCFNumberFormatterDecimalStyle,
    // 货币
    NSNumberFormatterCurrencyStyle = kCFNumberFormatterCurrencyStyle,
    // 百分比
    NSNumberFormatterPercentStyle = kCFNumberFormatterPercentStyle,
    // 科学计数法
    NSNumberFormatterScientificStyle = kCFNumberFormatterScientificStyle,
    // 中文
    NSNumberFormatterSpellOutStyle = kCFNumberFormatterSpellOutStyle,
};

```

示例：

```objc
NSNumber *number1 = @1234;
NSNumberFormatter *formatter = [[NSNumberFormatter alloc] init];
[formatter setNumberStyle:NSNumberFormatterPercentStyle];
NSString *string = [formatter stringFromNumber:number1];
NSLog(@"string = %@", string);
```


<span id = "change">
###类型转换


```objc

// 给定一个number转换成string
- (NSString *)stringFromNumber:(NSNumber *)number;
// 给定一个string转换成number
- (NSNumber *)numberFromString:(NSString *)string;
```

示例:

```objc
NSNumber *number1 = @1234;

NSNumberFormatter *formatter = [[NSNumberFormatter alloc] init];
[formatter setNumberStyle:NSNumberFormatterPercentStyle];

// 相互转换
NSString *string = [formatter stringFromNumber:number1];

NSNumber *number = [formatter numberFromString:string];

NSLog(@"string = %@", string);
NSLog(@"number = %@", number);
```
