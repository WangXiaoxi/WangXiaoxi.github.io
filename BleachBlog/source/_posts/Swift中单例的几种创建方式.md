---
title: Swift中单例的几种创建方式
date: 2017-01-12 01:41:27
tags:
---

# 单例
## 动画库`Spring`中，ImageLoader的单例实现

>**Spring** [https://github.com/MengTo/Spring](https://github.com/MengTo/Spring)

```
public class ImageLoader {
    public class var sharedLoader: ImageLoader {
        struct Static {
            static let instance: ImageLoader = ImageLoader()
        }
        return Static.instance
    }
}
```

## 类似于系统`default`的单例模式实现

>Alamofire 中，SessionManager的default实现 [https://github.com/Alamofire/Alamofire](https://github.com/Alamofire/Alamofire)

``` 
open class SessionManager {
   open static let `default`: SessionManager = {
        let configuration = URLSessionConfiguration.default
        configuration.httpAdditionalHeaders = SessionManager.defaultHTTPHeaders
        return SessionManager(configuration: configuration)
   }()
}
```

## Swifter Tips中所提到的单例实现
### Swift 3 之前的通常写法

```
class MyManager {
    class var sharedManager: MyManager {
        struct Static {
            static var onceToken: dispatch_once_t = 0
            static var staticInstance: MyManager? = nil
        }
        
        dispatch_once(&Static.onceToken) {
            Static.staticInstance = MyManager()
        }
        
        return Static.staticInstance!
    }
}
```

> 注: Swift 3 中移除了dispatch_once, 这种方式只对Swift 3 之前的版本有效。

### 同于Alamofire的方式

```
class MyManager {
    class var shared: MyManager {
        struct Static {
            static let sharedInstance: MyManager = MyManager()
        }
        return Static.sharedInstance
    }
}
```

### Swift 1.2 之前的最佳方法
>swift 1.2 之前 `class` 不支持存储格式的 `property`，定义一个只存在一份的属性时，只能定义在全局的 **scrope** 中。并且此变量只在当前文件中可以被访问。

```
private let sharedInstance = MyManager()

class MyManager {
    class var shared: MyManager {
        return sharedInstance
    }
}
```

### Swift 1.2 之后的改进
>swift 1.2 之后，若无特别需求，推荐以下方式

```
class MyManager {
    static let shared = MyManager()
    private init() {}
}
```

变量初始化时，Apple将会把这个初始化包装在一次`swift_once_block_invoke`中以保证唯一性。所有的全局变量都会在底层使用类似`dispatch_once`的方式，确保只以`lazy`的方式初始化一次。

标记`init`为私有方法保证了类型单例的唯一性



