## 返回值 & 函数 & 新的字符串
```
//函数
//返回值为 Int
fun function() : Int {
        //Kotlin 新的字符串，保留原格式
        var string : String = """
                www.ww ww
            w,w111111，     11
        """
        println(string)
        return 0;
    }
```
## 赋值 & assignment
```
fun functionToAssignment() : String {
        var number : Int = 10
        //assignment
        var string : String = "number = $number"
        println(string)
        return string
    }
```
## If & else 
```
fun functionToIfElse() : String {

        var numberA : Int = 10

        var numberB = 30

        var maxNumber : Int = 0

        if (numberA > numberB) maxNumber = numberA

        var minNumber : Int

        if (numberA > numberB) {
            minNumber = numberB
        } else {
            minNumber = numberA
        }

        return "mixNumber : $minNumber ,maxNumber : $maxNumber"
    }
```








