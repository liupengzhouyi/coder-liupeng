# 创建 枚举类

```
package liupengstudy.cn.learnapp01

enum class Direction {
    NORTH, SOUTH, WEST, EAST
}
```

## 应用代码

```
var direction : Direction = Direction.SOUTH

        var direction1 : Direction = Direction.NORTH
        var direction2 : Direction = Direction.EAST
        var direction3 : Direction = Direction.SOUTH
        var direction4 : Direction = Direction.WEST

        if (direction.equals(direction3)) {
            println("枚举类型相同")
        } else {
            println("枚举类型不同")
        }
```

## 遍历枚举

```
for (d in Direction.values()) {
            println(d)
        }
```


