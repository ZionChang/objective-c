#延展


延展主要是为相应的类添加其私有属性,以及私有方法.

比如我们现在创建一个Person类,我们想把我们的age以及birthday进行私有

只要如下即可,在.m文件

```objc
#import "Person.h"

@interface Person ()

@property (nonatomic, assign) int age;
@property (nonatomic, assign) NSString *birthday;

@end

@implementation Person

@end
```

大家已经注意到,在@implementation上面多了一个@interface,在这里面我们就可以进行私有属性以及私有方法的定制了,并且外部是无法进行访问的.