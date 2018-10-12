# 目前没有在程序中遇到常量与变量的BUG所以，不做重点
* var 这是变量
* let 这是常量
## 实例代码
```
 func paly() -> () {
        var number = 10
        
        let num = 20
        
        number = num
        
//        num = number
    }
``` 
## 附录
### 当一个变量在程序中没有用到修改时，代码会提示将var转变为let
```
func add() -> () {
        
        var a = 10
        
        let b = 20
        
        print(a + b)
    }
```