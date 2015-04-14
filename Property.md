
#属性

我们之前都是通过手动编写setter以及getter方法来进行成员变量的访问,而属性就可以便利的为我们提供这些,并且属性会自动生成带下划线的成员变量。

##格式如下

```objc
// 在Person.h文件增加了两个属性

@interface Person : NSObject

@property NSString *firstName;
@property NSString *lastName;


@end

```

申明这两个属性之后,我们就可以直接使用getter以及setter方法,或者直接使用点语法

##get&set

```objc
Person *person = [[Person alloc] init];
// getter
NSString *firstName = [person firstName];
// setter
[person setFirstName:@"Jone"];
```

##关键字讲解

```objc
 @property

 第一类：内存管理相关
     assign  :  缺省值   修饰基本数据类型和delegate对象
     retain  :  对象类型
     copy    :  对象类型（在遵守<NSCoping>情况下）
 第二类：线程相关
     atomic   :   缺省值 ，关心线程安全，通常用于多线程中
     nonatomic:  不关心线程安全，通常用于单线程中
 第三类：
     readwrite: 读写 缺省值
     readonly:  只读  (只提供getter方法，不提供setter方法)

 getter 、setter:重定义getter和setter方法名

 ARC模式下：
 weak   相当于  assign   相当于，但不等价 注意
 strong 相当于  retain   相当于

```


##自定义合成变量名

在iOS5之后,如果不进行变量名合成,系统会自动生成带下划线的成员变量,接下来我们自定义合成变量名

在Person.m我们可以看到可以直接使用_firstName;

```objc
@implementation Person
- (instancetype)init
{
    self = [super init];
    if (self) {
    // 使用系统生成的带下划线的名字
        _firstName = @"hello";
    }
    return self;
}

@end
```

如果自定义该变量名就使用@synthesize关键字,示例:

```objc
@implementation Person
// 重新合成名字
@synthesize firstName = first;
- (instancetype)init
{
    self = [super init];
    if (self) {
    // 使用合成的名字
        first = @"hello";
    }
    return self;
}
@end
```

大家可以实验,如果当前我创建一个Student类继承与Person类,那么在里面<font color = "red">无法使用_firstName</font>

```objc
  _firstName = @"asdf";
  // 报错原因
  Use of undeclared identifier '_firstName'
```

这个时候如果使用上面的关键字就可以解决,否则就使用self.firstName,下面解决方法

```objc
@implementation Student

@synthesize firstName = _firstName;

- (instancetype)init
{
    self = [super init];
    if (self) {
        _firstName = @"asdf";

    }
    return self;
}

@end

```


