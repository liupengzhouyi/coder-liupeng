# 一个for循环的实例
## 代码部分
```
func demo5() {
        // [0-5)
        for i in 0..<5 {
            print(i)
        }
        
        // [0-5]
        for i in 0...5 {
            print(i)
        }
    }
```
## 如何反序遍历
```
//for循环反序遍历
    func demo6() {
        for i in (0..<4).reversed() {
            print(i)
        }
    }
```