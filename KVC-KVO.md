
#KVC-KVO(键盘编码-键值观察)

##KVC (key-value-coding)

方法列表

```objc
// 获取通过key
- (id)valueForKey:(NSString *)key;
// 设置值
- (void)setValue:(id)value forKey:(NSString *)key;
- (id)valueForKeyPath:(NSString *)keyPath;
- (void)setValue:(id)value forKeyPath:(NSString *)keyPath;
```

首先我们创建一个类

```objc
@interface Student : NSObject

@property (nonatomic, strong) NSString *name;
@property (nonatomic, strong) NSString *sex;
@property (nonatomic, strong) NSString *code;
@property (nonatomic, assign) CGPoint position;

@end
```

按照我们以前的赋值方式,我们肯定会这样做

```objc
Student *stu = [[Student alloc] init];
// 进行赋值
stu.name = @"zhangsan";
stu.sex = @"male";
```

而如果使用KVC方式就可以使用以下代码

```objc
// 等价于
[stu setValue:@"zhangsan" forKey:@"name"];
[stu setValue:@"name" forKey:@"sex"];
```

这两种方式在这里可以说是等价的,但是需要注意如果设置值对应的key不存在属性列表中,那么会存在<font color = "red">崩溃现象</font>,崩溃信息如下:

```objc
[stu setValue:@"helo" forKey:@"phone"];

reason: '[<Student 0x100206af0> setValue:forUndefinedKey:]: this class is not key value coding-compliant for the key phone.'
```

所以,一定要注意key是存在属性列表中才可以使用KVC

接着我们来看另外一种情况,如果这个学生拥有一个老师,他想去设置老师对应的值,利用KVC应该怎么实现呢

```objc
@interface Teacher : NSObject

@property (nonatomic, assign) CGPoint position; // 位置
@property (nonatomic, strong) NSString *name;   // 姓名

@end
```

然后我们为学生添加一个老师属性

```objc
@property (nonatomic, strong) Teacher *teacher;
```
最后我们在main函数中

```objc
Teacher *teacher = [[Teacher alloc] init];
// 建立关联
stu.teacher = teacher;
// 间接设置
stu.teacher.name = @"Jone";
// 利用KVC,利用属性名+点+相应的属性名
[stu setValue:@"Mary" forKeyPath:@"teacher.name"];
// 访问
NSLog(@"%@", stu.teacher.name);
```

##KVO (key-value-observe)

有时我们需要监听一些属性的改变,然后执行相应的操作,现在我们来模拟一个操作,比如学生发生老师的位置发生改变的时候,就进行相应的操作.

同样我们在学生类中添加方法

```objc
#import "Student.h"

@implementation Student

- (void)watchTeacherPositionChanged
{
// 注册
// 1:观察者
// 2:路径
// 3:选项
// 4:一般写 nil 或者 NULL
    [self addObserver:self
           forKeyPath:@"teacher.position"
              options:NSKeyValueObservingOptionNew | NSKeyValueObservingOptionOld
              context:@"position"];
    
    }

```

其次直接在Student.m文件重写该方法

```objc
// 当老师的位置发生改变时,自动调用该方法
- (void)observeValueForKeyPath:(NSString *)keyPath ofObject:(id)object change:(NSDictionary *)change context:(void *)context
{
    // 从change这个字典中获取相应的值
    
    if ([keyPath isEqualToString:@"teacher.position"]) {
        NSValue * point = change[@"new"];
        CGPoint newPoint = [point pointValue];
        if (newPoint.x == self.position.x && newPoint.y == self.position.y) {
            NSLog(@"%@说:老师来了，快点关QQ", self.name);
        } else {
            NSLog(@"%@说:诶，老师走了，继续！", self.name);
        }
    }

}

```

然后在dealloc方法中

```objc
- (void)dealloc
{
// 移除监听
    [self removeObserver:self forKeyPath:@"teacher.position"];
}

```

最后在main函数中调用

```objc
Student * stu1 = [[Student alloc] init];
stu1.name = @"lisi";
stu1.position = CGPointMake(1, 1);
   
   
Student * stu2 = [[Student alloc] init];
stu2.position = CGPointMake(4, 2);
stu2.name = @"zhangsan";
   
// KVC KVO
Teacher * teacher = [[Teacher alloc] init];
   
stu1.teacher = teacher;
stu2.teacher = teacher;
// KVO
[stu1 watchTeacherPositionChanged];
[stu2 watchTeacherPositionChanged];
teacher.position = CGPointMake(1, 1);
teacher.position = CGPointMake(1, 2);
teacher.position = CGPointMake(4, 2);

```