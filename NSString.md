NSString 为不可变字符串，大家可以注意查看头文件，任何针对字符串改变的方法都拥有一个NSString *返回值，如果想获得改变的字符串就必须去进行接收。

>初始化方法

```objc
// 直接赋值
NSString *string1 = @"hello world";
// 利用格式化字符
NSString *string2 = [NSString stringWithFormat:@"%@", string1];
// 利用C语言字符串
char str[] = "hello world";
NSString *string3 = [NSString stringWithUTF8String:str];
```

>查找

```objc
NSString *string = @"www.baidu.com";
// 是否含有前缀
BOOL hasHttp = [string hasPrefix:@"http://"];
// 是否含有后缀
BOOL hasCom = [string hasSuffix:@"com"];
// 是否包含,返回一个结构体类型
// 其中如果location为NSNotFound 或者 length为0，说明没有找到
NSRange range = [string rangeOfString:@"baidu"];
if (range.location == NSNotFound) {
 NSLog(@"no");
} else {
 NSLog(@"yes");
```

>拼接

```objc

- (NSString *)stringByAppendingString:(NSString *)aString;
- (NSString *)stringByAppendingFormat:(NSString *)format, ... NS_FORMAT_FUNCTION(1,2);

// 都在字符串末尾进行拼接
NSString *string = @"hello";
// 直接追加
NSString *newString = [string stringByAppendingString:@"world"];
// 以格式化追加
NSString *str = [string stringByAppendingFormat:@"say:%@", newString];

```

>截取

```objc
- (NSString *)substringFromIndex:(NSUInteger)from;
- (NSString *)substringToIndex:(NSUInteger)to;
- (NSString *)substringWithRange:(NSRange)range;

// 示例

// 注意字符串下标是从0开始
NSString *string = @"www.baidu.com";
// 从第4个开始截取，包括第4个
NSString *newString1 = [string substringFromIndex:4];
// 截取到第4个，不包括第4个
NSString *newString2 = [string substringToIndex:4];
// 从第2个开始截取，截取4个
NSString *newString3 = [string substringWithRange:NSMakeRange(2, 4)];

```

>替换

```objc
NSString *string = @"www,baidu,com";
NSString *newString = [string stringByReplacingOccurrencesOfString:@"," withString:@"."];
```

>大小写转换

```objc
NSString *string = @"hello WORLD";
NSLog(@"%@", string.lowercaseString);
NSLog(@"%@", string.uppercaseString);
```

>数值转换

```objc

@property (readonly) double doubleValue;
@property (readonly) float floatValue;
@property (readonly) int intValue;
@property (readonly) NSInteger integerValue NS_AVAILABLE(10_5, 2_0);
@property (readonly) long long longLongValue NS_AVAILABLE(10_5, 2_0);
@property (readonly) BOOL boolValue NS_AVAILABLE(10_5, 2_0);

// 意味这些都生成相应的getter方法，所以我们根据自己的要求获取相应的Value

NSString *string = @"1234";
int value = [string intValue];

```

>获取字符

```objc
NSString *string = @"hello world";
unichar ch = [string characterAtIndex:1];
NSLog(@"ch = %c", ch);

```


>长度

```objc
NSString *string = @"hello world";
NSUInteger length = [string length];

```
>比较

```objc

NSString *string = @"hello world";
NSString *newString = [NSString stringWithFormat:@"%@", string];
// 第一种地址比较
if (string == newString) {
    NSLog(@"地址相同");
} else {
	 NSLog(@"地址不同");
}
// 第二种值比较
if ([string isEqualToString:newString]) {
	 NSLog(@"内容相同");
} else {
	 NSLog(@"内容不同");
}
  
// 第三种compare比较
  
if ([string compare:newString] == NSOrderedSame) {
	 NSLog(@"相同");
} else if ([string compare:newString] == NSOrderedAscending) {
	 NSLog(@"升序");
} else {
	 NSLog(@"降序");
}


```
