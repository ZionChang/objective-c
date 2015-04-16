
#观察者模式

##概念

>观察者模式（Observer）完美的将观察者和被观察的对象分离开。举个例子，用户界面可以作为一个观察者，业务数据是被观察者，用户界面观察业务数据的变化，发现数据变化后，就显示在界面上。面向对象设计的一个原则是：系统中的每个类将重点放在某一个功能上，而不是其他方面。一个对象只做一件事情，并且将他做好。观察者模式在模块之间划定了清晰的界限，提高了应用程序的可维护性和重用性。
观察者设计模式定义了对象间的一种一对多的依赖关系，以便一个对象的状态发生变化时，所有依赖于它的对象都得到通知并自动刷新。

##实现


这三步必须实现

* 添加观察者
* 发送通知
* 移除观察者

讲解之前我们首先了解4个方法,我们也要使用到系统的一个单例NSNotificationCenter

```objc
// 获取系统通知中心
+ (NSNotificationCenter *)defaultCenter;
// 添加观察者
// 参数1：观察者
// 参数2：观察者的方法
// 参数3：观察的通知姓名
// 参数3：传递的参数
- (void)addObserver:(id)observer selector:(SEL)aSelector name:(NSString *)aName object:(id)anObject;
// 发送通知
// 参数1：通知的姓名
// 参数2：通知的参数
- (void)postNotificationName:(NSString *)aName object:(id)anObject;
// 移除观察者
- (void)removeObserver:(id)observer;

```


接下来我们模拟一个通知,首先我们创建两个类Student以及Teacher,当铃声响起的时候,老师就调用一个行为,而学生也调用一个行为,相同于一直在监听某个事物

```objc
@interface Student : NSObject

@end
@interface Teacher : NSObject

@end
```

接着我们在.M文件分别写上代码:

```objc
#import "Student.h"

@implementation Student

- (void)dealloc
{
	// 第三步,移除观察者
    [[NSNotificationCenter defaultCenter] removeObserver:self];
}

- (instancetype)init
{
    self = [super init];
    if (self) {
        // 第一步,添加通知
        [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(ring) name:@"RING" object:nil];
    }
    return self;
}

- (void)ring
{
    NSLog(@"放学了!");
}

@end
```

老师实现文件也是一样,唯一不同的是

```objc
- (void)ring
{
    NSLog(@"下班了!");
}
```



然后我们在mian函数中创建相应的对象,并且发送通知

```objc
// 创建对象
Teacher *teacher1 = [[Teacher alloc] init];
Student *stu1 = [[Student alloc] init];
   
// 发送通知
[[NSNotificationCenter defaultCenter] postNotificationName:@"RING" object:nil];
```
打印结果

```objc
2015-04-15 22:57:44.310 OC_Lesson5[2257:219593] 下班了!
2015-04-15 22:57:44.311 OC_Lesson5[2257:219593] 放学了!
```
