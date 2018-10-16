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

# 但是更多的情况是，对一个数组，集合，字典的遍历了！

# 



