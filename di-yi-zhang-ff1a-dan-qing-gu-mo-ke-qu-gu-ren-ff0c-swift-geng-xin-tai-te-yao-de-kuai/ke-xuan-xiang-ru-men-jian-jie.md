# 可选项

可选项就是类似于定义了一个在Java程序中的object，并负值null.

## 代码

```
func demoForOptional() -> () {
        // 1。 原始的可选项定义
        // none 没有值，或者 某一类h值
        let x : Optional = 10

        //2. 简单的定义
        // ‘？’来指定一个可选项的值，
        let y : Int? = 20 // nil

        //输出
        print(x!)

        print(y!)

        // 为每一个！负责，即有确定的值
        print(x! + y!)
    }
```



