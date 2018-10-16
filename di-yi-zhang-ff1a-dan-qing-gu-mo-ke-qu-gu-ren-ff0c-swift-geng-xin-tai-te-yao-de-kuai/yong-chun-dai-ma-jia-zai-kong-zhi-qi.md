# 用纯代码加载控制器

## 代码
```
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // Override point for customization after application launch.
        
        //实例话window
        window = UIWindow()
        window?.backgroundColor = UIColor.red
        
        //设置根控制器
        let vc = ViewController()
        window?.rootViewController = vc
        
        //w让window可见
        window?.makeKeyAndVisible()
        
        return true
    }
```

## 在哪里添加
## class AppDelegate
