# IDEA 测试

## 项目导入包

* junit-4.12.jar
* hamcrest-core-2.1.jar

*我希望你不要问我如何导入jar包，请自己找教程，本教程不是面向新手的，因为赚不了钱，本人这里郑重声明，希望信任不要入坑，宁可去炒股，莫学计算机。*

## 创建一个类

你要随便实现一点点的功能，因为我们要测试他的功能。

比如我创建的是这样的

### 类名

AddClass

### 方法

|  方法名 | 方法功能 | 参数 | 返回值 | 作者 | 时间 |
| --- | --- | --- | --- | --- | --- |
| AddNumber | 数字相加 |  int型数字 * 2 | int型数字 * 1 | 刘鹏 | 2019-2-27 11:21 |


### 代码


```
public class AddClass {

    public int AddNumber(int numbera, int numberb) {
        int number = numbera + numberb;
        return  number;
    }
    
}
```


## 创建一个测试文件夹

1. 新建文件夹-test

![](/assets/屏幕快照 2019-02-27 上午11.30.24.png)

2. 把该文件夹作为测试文件夹

![](/assets/屏幕快照 2019-02-27 上午11.30.45.png)

3. 效果

![](/assets/屏幕快照 2019-02-27 上午11.30.57.png)

## 生成测试类

快捷键 command + shift + T

![](/assets/屏幕快照 2019-02-27 上午11.53.30.png)


然后就会有测试类生成。

![](/assets/屏幕快照 2019-02-27 上午11.53.47.png)


测试类的代码如下


```
package TEST;

import org.junit.After;
import org.junit.Before;
import org.junit.Test;

import static org.junit.Assert.*;

public class AddClassTest {

    @Before
    public void setUp() throws Exception {
    }

    @After
    public void tearDown() throws Exception {
    }

    @Test
    public void addNumber() {
    }
}
```

很显然，这个啥用都没有！我们需要对他进行社会主义改造！

最后，他是这个样子的！


```
package TEST;

import org.junit.After;
import org.junit.Before;
import org.junit.Test;

import static org.junit.Assert.*;

public class AddClassTest {

    @Before
    public void setUp() throws Exception {
        System.out.println("开始测试");
    }

    @After
    public void tearDown() throws Exception {
        System.out.println("结束测试");
        System.out.println("\n");
    }

    @Test
    public void addNumberI() {
        System.out.println("我不知道这是方法有什么用？");
    }

    @Test
    public void addNumberII() {
        System.out.println("我现在知道有什么有了！");

        AddClass addClass = new AddClass();

        System.out.println(addClass.AddNumber(123,345));
    }
}
```


## 测试类的了解

* @Test：把一个方法标记为测试方法
* @Before：每一个测试方法执行前自动调用一次
* @After：每一个测试方法执行完自动调用一次
* @BeforeClass：所有测试方法执行前执行一次，在测试类还没有实例化就已经被加载，所以用static修饰
* @AfterClass：所有测试方法执行完执行一次，在测试类还没有实例化就已经被加载，所以用static修饰
* @Ignore：暂不执行该测试方法!
[](/assets/屏幕快照 2019-02-27 上午11.30.24.png)