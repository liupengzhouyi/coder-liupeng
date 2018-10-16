# 南京女子图鉴

![](/assets/佐藤遥希.jpeg)

# getter & setter

* 在Swift中，getter & setter很少使用

实例代码：


```
class Person: NSObject {
    
    var _name : String?
    
    var name : String? {
        get {
            //返回成员变量
            return self._name
        }
        set {
            // 使用 _成员变量 记录 值
            self._name = newValue
        }
    }
}

```






