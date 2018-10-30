# Commons DbUtils 数据库连接
## 硬需求
* jar包：Commons DbUtils：JDBC Utility Component
* [jar包下载地址](https://commons.apache.org/proper/commons-dbutils/)
## 说明：
Commons DbUtils库是一小组类，旨在简化 JDBC的使用。JDBC资源清理代码是平凡的，容易出错的工作，所以这些类从代码中抽象出所有清理任务，首先让你了解你真正想用JDBC做的事情：查询和更新数据。

## 使用DbUtils的一些优点是：
* 没有资源泄漏的可能性。正确的JDBC编码并不困难，但它既费时又乏味。这通常会导致可能难以追踪的连接泄漏。
* 更清晰，更清晰的持久性代码。将数据保存在数据库中所需的代码量大大减少。剩余的代码清楚地表达了您的意图，而不会混淆资源清理。
* 从ResultSet自动填充JavaBean属性。您无需通过调用setter方法手动将列值复制到bean实例中。ResultSet的每一行都可以由一个完全填充的bean实例表示。
## 使用：
1. IDEA 导入包：
![](/assets/屏幕快照 2018-10-30 下午4.42.38.png)
2. 


