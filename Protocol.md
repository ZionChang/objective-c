#协议

OC不能多继承,也没有抽象类这个概念的存在,但是却拥有协议

>1. Protocol：就一个用途,用来声明一大堆的方法（不能声明成员变量）,不能写实现。
2. 只要某个类遵守了这个协议,就拥有了这个协议中的所有方法声明。
3. 只要父类遵守了某个协议,那么子类也遵守。
4. Protocol声明的方法可以让任何类去实现,protocol就是协议。
5. OC不能继承多个类（单继承）但是能够遵守多个协议。继承(:),遵守协议（< >）
6. 基协议：<NSObject>是基协议,是最根本最基本的协议,其中声明了很多最基本的方法。
7. 协议可以遵守协议,一个协议遵守了另一个协议,就可以拥有另一份协议中的方法声明。

* [协议的定义](#definition)
* [如何遵守协议](#how)
* [举例](#example)
* [委托设计模式](#delegate)


<span id = "definition">
##协议的定义
```objc

@protocol 协议名称 <NSObject>

//方法声明列表

@end;
```

<span id = "how">
##如何遵守协议

（1）类遵守协议

```objc
@protocol 类名：父类名 <协议名称1,协议名称2>

@end
```
（2）协议遵守协议

```objc
@protocol 协议名称 <其他协议名称>

@end;

```
3.协议方法声明中的关键字

```objc
（1）required （默认）要求实现,若没有实现则警告但不报错

（2）Optional 不要求实现
```

4.定义变量时遵守协议的限制

```objc

类名<协议名称> *变量名    NSObject<Myprotocol> *obj;

Id  <协议名称>  变量名   id  <Myprotocol> obj1;

```

 

5.Property中声明的属性也可以做遵守协议的限制

```objc
@property (nonatomic ,strong ) 类名<协议名称> *属性名；
@property (nonatomic ,strong ) id<协议名称>  属性名；
```

<span id = "example">
##举例

接下来我们创建一个协议,我们在Person.h文件中直接写一个协议

```objc

@protocol WorkerProtocol<NSObject>

// 必须工作8个小时
@required
- (void)workEightHour;

// 可以中途上厕所
@optional
- (void)goToWC;

@end

@interface Person : NSObject

@end
```

然后我们让Person遵守这个协议

```objc
@interface Person : NSObject <WorkerProtocol>

@end
```

最后在Person.m文件中实现协议中必须实现的方法,可选的方法就看情况而定.

```objc
- (void)workEightHour
{
    NSLog(@"ok");
}
```

<span id = "delegate">
##委托设计模式

首先我们来创建一个Worker继承与Person,我们来模拟租房子的过程,其中我们需要创建一份协议,并且让中介(Agent)来遵守这份协议

```objc
#import "Person.h"
#import "RIMIProtocol.h"

@protocol RentProtocol <NSObject>

// 我需要代理人告诉我房子的一些信息
- (NSString *)tellMeSomeInformation:(NSString *)information
                        money:(double)money;


@end

@interface Worker : Person <RIMIProtocol>
// 设置一个代理人,主要使用assgin,并且使用id类型,因为不定义只有中介能够帮我们找寻房子
@property (nonatomic, assign) id<RentProtocol> delegate;

// 寻找一个中介
- (void)findAAgent;

@end

```

实现文件

```objc
- (void)findAAgent
{
    // 创建一个代理人
    Agent * agent = [[Agent alloc] init];
    // 进行关联
    self.delegate = agent;
    // 判断当前代理人是否存在以及是否遵守这份协议
    if (self.delegate && [self.delegate conformsToProtocol:@protocol(RentProtocol)]) {
    	 // 最后让其调用协议中的方法
        NSString *result = [self.delegate tellMeSomeInformation:@"两室一厅" money:2000];
        NSLog(@"result = %@", result);
    }
    [agent release];
}
```

创建一个Agent继承与Person,并且遵守该协议

```objc
#import "Person.h"
#import "Worker.h"

@interface Agent : Person <RentProtocol>

@end
```

然后实现

```objc
#import "Agent.h"

@implementation Agent

- (NSString *)tellMeSomeInformation:(NSString *)information
                        money:(double)money
{
    return [NSString stringWithFormat:@"终于找到了, 两室一厅，价格是2200，我给谈一下，可以给你优惠100"];
}

@end
```

最后我们在main函数中调用即可

```objc
Worker * worker = [[Worker alloc] init];
[worker findAAgent];
```