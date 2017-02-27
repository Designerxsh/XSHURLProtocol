#Swift URLProtocol

你可能会遇到这样的需求：
> 在特定的request上做特殊配置。  
> 忽略请求，直接返回你的response。  
> 拦截图片加载请求，让数据直接从本地文件加载。  
> 重定向网络请求。  
> 网络性能检测。  
> ……

在不影响和掺杂现有逻辑的基础上来实现这些功能，你需要了解`URLProtocol`。
***
iOS网络请求离不开Foundation库的[URL Loading System](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/URLLoadingSystem/URLLoadingSystem.html)，`URLProtocol` 正是苹果为我们提供的[URL Loading System](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/URLLoadingSystem/URLLoadingSystem.html)的一部分。整个URL Loading System 包含以下内容：

![URL Loading System](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/URLLoadingSystem/Art/nsobject_hierarchy_2x.png)
 
看名字你可能以为`URLProtocol`是个协议，但其实它是个abstract类，所以不能够直接使用，必须被子类化之后才能使用。有了它，我们就可以在不改动应用中的网络调用层的逻辑上，实现改变URL加载行为的全部细节。

##使用方法
###实例化URLProtocol
实例化你的URLProtocol  

```
class XSHURLProtocol: URLProtocol {}
```

###注册URLProtocol

```
NSURLSessionConfiguration * config = [NSURLSessionConfiguration defaultSessionWithURLProtocolConfiguration];  
NSArray *protocolArray = @[[XSHURLProtocol class]];  
config.protocolClasses = protocolArray;  
NSURLSession *session = [NSURLSession sessionWithConfiguration:config];
```

###必须实现的方法
			