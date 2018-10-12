# 闭包的定义
## 闭包是自包含的代码块，可以在代码中被传递和使用
### 闭包可以捕获和存储它所在的上下文的任意变量和常量，
## 闭合并包裹着这些数据量

# 闭包的格式
```
//没有函数名称 {
//    (c参数) -> String(返回类型) in
//    code
//}
```
# 实例
```
let numbers = [1800, 756, 9800]

let strResult = numbers.map{
    (number : Int) -> String in
    
    var outPut : String = ""
    var num = number
    
    while (num > 0) {
        outPut = String(num % 10) + "." + outPut
        num /= 10
    }
    
    return outPut
}

print(strResult)
```



