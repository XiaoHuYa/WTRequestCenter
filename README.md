WTRequestCenter
===============

```bash
```
升级中,暂无可参阅文档,敬请期待...

# 创建一个请求

```objective-c

NSURLRequest *request =  [[WTNetWorkManager sharedKit] requestWithMethod:@"GET" URLString:_urlTextField.text parameters:nil error:nil];
[[WTNetWorkManager sharedKit] taskWithRequest:request finished:^(NSData *data, NSURLResponse *response) {
NSString *string = [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
if (string) {
_textView.text = string;
}
} failed:^(NSError *error) {

}];

```


需要版本  
===============
iOS 7.0


##  UIKit+WTRequestCenter
这里面提供了许多UIKit的扩展方法
- UIImageView的图片缓存
- UIImage的播放gif+图片缓存
- UIButton的图片缓存
- UIColor的快速创建
- UIDecive的扩展（uuid调用）
- UIWebView的缓存扩展（暂时不支持网页游戏的缓存）
- UIScreen 提供了一些适配屏幕的好方法，具体看注释
- UIApplication 提供了版本号和build号的获取
- WTNetworkActivityIndicatorManager提供了网络指示器

## Communication  
- 如果你**发现bug**,<a href="https://github.com/swtlovewtt/WTRequestCenter/issues">打开右侧的问题</a>
- 如果你**想做出贡献**,<a href="https://github.com/swtlovewtt/WTRequestCenter/pulls">提交一个推（pull）的请求</a>
- 如果你**有功能需求**,<a href="https://github.com/swtlovewtt/WTRequestCenter/issues">打开问题</a>








##iOS编程规范

 - 使用auto layout 来做UI，这样的话就能适配各种屏幕尺寸（size classes建议用any width,any height 这样适配的是所有的屏幕）
 - 头文件能不import就不要import文件，节省编译时间.
 - 用枚举来表示状态,选项,状态码
 - 本地如果要读取实例变量就直接调用( _var ),如果要写入就调用属性的方法,这样做效率比较高
 - 懒加载模式可以节约内存
 - 命名要规范，成员变量前面加上下划线（NSString *_var）这么做的目的是区分成员变量和局部变量
 - 提交代码之前尽量去掉或者注释掉输出，多注意，方便debug.
 - 协议用"#pragma mark  <protocol>"来标记代码，这样方便快速跳到protocol里面查看方法
 - 头文件要有一定量的注释.
 - 不使用prefix header 文件,节省编译时间.
 - 图片管理使用Images.xcassets.
 - 使用@import framework 就不需要手动导入改库了。
 - View千万不要处理业务逻辑，只适合做UI
 - 能用OperationQueue的地方不要用GCD.
 - 必要的时候对一个对象设计一个初始化方法
 - 尽量使用不可变的数据
 - 用categories把类的实现断开成不同的区域
 - 用Zombies来帮助debug内存问题
 - 常量不要用宏定义指定，用静态常量声明，这样做数据的数值就不会产生变化，宏定义里面有undefine
 - 用分析去查看内存用错的地方.
 - 用Profile测试程序的性能.
 - 使用xib来调整自动布局. 不要使用 storyboard（简称sb），因为大程序里面sb文件会很大，编译特别慢，影响开发效率。

##MVC
###View的做法
View的功能就是展示UI，不储存任何数据，不参与任何业务逻辑
View的数据来源是Datasource，交互事件是Delegate

###Controller
程序的中心，对Model和V有绝对的控制权，业务的核心。

###Model
Model要求不高，用原生数据类型或者jsonModel生成的都可以。
通常情况下Controller去修改model，修改完后该刷新UI刷新UI。


###总结
 - Controller对Model和View的绝对控制权。
 - Model通过Notification来通知Controller数据发生了变化。
 - View通过Datasource或者Delegate来告知Controller自己发生了变化/是否需要发生变化。
 - Model和View不直接通信，没有任何关系。
 - Controller之间可以互相帮忙，大量的Controller结合起来就形成了一个完整的程序
