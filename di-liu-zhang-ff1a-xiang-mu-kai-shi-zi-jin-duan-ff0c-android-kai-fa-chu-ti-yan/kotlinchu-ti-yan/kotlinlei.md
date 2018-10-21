# Kotlin Class

* init()
这是主构造器

* 构造函数
在Kotlin中不分构造函数，只有**主构造器**与**第二构造器**

* 主构造器
**init()方法**

* 第二构造器
关键字：**constructor**

* getter & setter

* 只读属性
在getter & setter 中 只写 getter 方法

* open
open： 代表开放，可以被继承

* 继承
使用“:”表示继承

* 复写
关键字：**override**

* 静态
Java中有静态static， 但是Kotlin不支持静态方法

* 单例模式
使用**全局变量**
使用**private**声明**主构造器**与**第二构造器**

* 全局变量

* 默认参数
```
//方法的默认参数
    fun printHello(name : String = "liupeng") {
        println("Hello! " + name)
    }


```
* 在Kotlin中，一切默认不可重写，如果你想改变，请添加关键字open
## 代码
### class Parent
```
package liupengstudy.cn.learnapp01

//open： 代表开放，可以被继承
open class Parent(name: String) {
    //初始化成员属性
    private var name: String = name
    //主构造器
    init {
        this.name = name
        println("---Parent---")
        println(this.name)
    }

    //第二构造器
    //该构造器 跳用 第一构造器
    constructor(value : Int):this("liupeng") {
        println("-------------------------")
        println("使用第二构造器")
        println("name:liupeng")
        println("传入参数: " + value)
        println("-------------------------")
    }

    //第二构造器
    //该构造器 调用 第二构造器
    constructor() : this("20")
    fun testForField() {
        println("-------------------------")
        println("使用第二构造器")
        println("调用第二构造器")
        println("传入参数: " + "null")
        println("-------------------------")
    }

    //open 表示该方法可以被复写
    open fun getName() : String {
        return this.name
    }

}
```
### class Child
```
package liupengstudy.cn.learnapp01

//继承
class Child(parentName : String, name : String) : Parent(parentName) {
    private var myName : String = name
    init {
        println("---Child---")
        println(this.myName)
    }

    public fun getFunction() {
        super.getName()
    }

    //复写方法
    override fun getName(): String {
        return this.myName
    }

    //只读属性
    val number : Int
        get() = 100

    //读写属性
    var string : String
        get() = string
        set(value) {
            string = value
        }

    //方法的默认参数
    fun printHello(name : String = "liupeng") {
        println("Hello! " + name)
    }

}


```




