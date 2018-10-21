# User类
## 代码 
```
class User(name: String, age: Int) {
    var name: String = name
    var age: Int = age
}
```

## 实例运行
```
//数据类
        var user1 : User = User("liupeng", 21)
        var user2 : User = User("liupeng", 21)

        println(user1)
        println(user2)
        //调用toString(), toString()调用hashcode(), 前面加上"类名@"

        println(user1.equals(user2))
```

## 运行结果
```
liupengstudy.cn.learnapp01.User@6bf2d08e
liupengstudy.cn.learnapp01.User@5eb5c224
false
```


## 重写方法
```
package liupengstudy.cn.learnapp01

class User(name: String, age: Int) {
    var name: String = name
    var age: Int = age

    override fun equals(other: Any?): Boolean {
        if (other is User) {
            if (this.name == other.name && this.age == other.age) {
                return true
            }
        } else {
            return false
        }
        return false
    }
}
```



