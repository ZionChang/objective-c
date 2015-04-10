# 方法与继承

##方法

OC中方法主要分为两种，一种+号开始的类方法，另一种就是-号开始的实例方法。

```objc
// 这就是上一章所讲到的创建对象所调用的两个方法，他们都是NSObject下面的方法。
+ (instancetype)alloc;	// 分配空间	
- (instancetype)init;	// 进行初始化
```

###自定义方法
接下来我们还是按照第一章所讲的步骤先创建一个Student类，然后为其添加一些独特的方法。

然后在.h文件中去声明两个方法

```objc
@interface Student : NSObject
{
    NSString *_name;
    int _age;
}

// 方法书写规范

/* 确定加号还是减号 (当前方法返回类型)方法名
 * 如果有参数接着书写冒号:(参数数据类型)变量名1 描述名:(数据类型)变量名2
 * 下面就书写了两个方法，一个是有参数有返回值的，一个是无返回值无参数的
 */

// 自定义初始化方法以 initWith开始
- (instancetype)initWithName:(NSString *)name age:(int)age;


- (void)sayHello;



```

然后进入.m文件我们分别实现这两个方法


```objc
#import "Student.h"

@implementation Student

- (instancetype)initWithName:(NSString *)name age:(int)age
{
	// 这三部在初始化方法中，必不可少，大家可以认为这是一个模板
    self = [super init];
    if (self) {
        // 要进行的赋值操作，全部在这里执行
    }
    return self;
}


- (void)sayHello
{
    
}

@end
```
完整的代码如下:

```objc

@implementation Student

- (instancetype)initWithName:(NSString *)name age:(int)age
{
    self = [super init];
    if (self) {
        // 要进行的赋值操作，全部在这里执行   
        _name = name;
        _age = age;
        
    }
    return self;
}


- (void)sayHello
{
    NSLog(@"hello world!");
}

@end

```

接着我们在.h文件中去声明一个+号方法 .m中实现该方法

```objc

// 类方法 + 号开始
+ (void)fly;


// 实现部分
+ (void)fly
{
    NSLog(@"Person can't fly!");
}


```

###方法调用


方法我们已经写好了
