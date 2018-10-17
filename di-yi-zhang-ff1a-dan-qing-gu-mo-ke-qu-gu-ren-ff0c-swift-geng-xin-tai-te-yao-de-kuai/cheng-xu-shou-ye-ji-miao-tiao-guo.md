# 当你打开APP
## 会有一个首页的广告，但是一般的广告都会设置几秒跳过
## 代码在哪里？
### AppDelegate
```
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // Override point for customization after application launch.
        
        sleep(3)
        
        return true
    }
```
## 如何设置
添加睡眠代码
```
sleep()3

```


