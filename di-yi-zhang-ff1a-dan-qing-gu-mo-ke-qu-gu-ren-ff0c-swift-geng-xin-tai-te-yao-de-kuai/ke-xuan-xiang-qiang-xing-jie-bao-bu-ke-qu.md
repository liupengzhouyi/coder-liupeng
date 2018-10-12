# 可选项的应用比较麻烦
## 寻找一种比较简单的方法
### 直接上代码
```
//对于强行解包
    // 使用 ‘？？’
    // 如果有值，使用值
    // 如果没有值， 使用？？后面的值
    func demo02(x : Int?, y : Int?) {

        print((x ?? 0) + (y ?? 0))
        
        //string
        let name : String? = "老王"
        print((name ?? "") + "你好！")
    }
```
## 判断值是否为nil
### if let 代码
```
// if let 连用， 判断对象的值是否为 nil
    func demo3() {
        let oName : String? = "老王"
        let oAge : Int? = 10
        
        // 原方法
        if oName != nil && oAge != nil {
            print(oName! + String(oAge!))
        } else {
            print("nameo或age为空")
        }
        
        //if let 连用
        if let name = oName, let age = oAge {
            print(name + String(age))
        } else {
            print("nameo或age为空")
        }
    }
```
## guard let 代码
```
//guard let
    func demo4() {
        let oName : String? = "老王"
        let oAge : Int? = 10

        // guard let 守护一定有值， 如果没有直接返回
        guard let name = oName, let age = oAge else {
            return
        }
        
        // 与if let 不同，他的值的作用域变得不一样
        // 可以降低分支
        print(name + String(age))
    }
```
