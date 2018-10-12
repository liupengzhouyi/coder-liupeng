# 关于Tomcat中的自带的数据库连接池
## Apache 有自家的数据库连接池DBCP
### 第一部，倒入包
#### 包名
1. Commons DBCP
2. Commons Collections
3. Commons Pool
#### 地址
Tomcat/lib/下
### 第二步， 修改配置文件
#### 路径
tomcat/conf/context.xml
#### 修改方式
添加
#### 内容
```
<Resource
            name="database_for_java_web"
            scope="Shareable"
            type="javax.sql.DataSource"
            factory="org.apache.tomcat.dbcp.dbcp2.BasicDataSourceFactory"
            url="jdbc:mysql://localhost:3306/database_for_java_web"
            driverClassName ="com.mysql.jdbc.Driver"
            username="root"
            password="lp184126"
    />
    <!--name: 映射名-->
    <!--url: 数据库地址-->
```
#### 路径
Java Web项目/web/WEB-INF/web.xml
#### 修改方式
添加
#### 内容

```
<!-- JDBC DataSources (java:comp/env/jdbc) -->
    <resource-ref>
        <description>The default DS</description>
        <res-ref-name>database_for_java_web</res-ref-name>
        <!--该名称必须与下面的描述文件中的一致-->
        <res-type>javax.sql.DataSource</res-type>
        <!--看看你的配置-->
        <res-auth>Container</res-auth>
    </resource-ref>
```

### 第三部， 编写测试servlet
#### 类名
DataSourceTestServlet
#### 路径
src.ServletPackage.DataSourceTestServlet
#### 代码
```
package ServletPackage;

import javax.naming.Context;
import javax.naming.InitialContext;
import javax.naming.NamingException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.sql.DataSource;
import java.io.IOException;
import java.io.PrintWriter;
import java.sql.Connection;
import java.sql.SQLException;

@WebServlet(name = "DataSourceTestServlet")
public class DataSourceTestServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        PrintWriter out = response.getWriter();

        try {
            Context context = new InitialContext();
            DataSource ds = (DataSource) context.lookup("java:/comp/env/database_for_java_web");
            Connection connection = ds.getConnection();
            if (connection != null) {
                out.print("get connection success!");
            }

        } catch (NamingException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        } catch (SQLException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}
```
### 在xml文件中修改
#### 路径
Java Web项目/web/WEB-INF/web.xml
#### 修改方式
添加
#### 代码
```
<servlet>
        <servlet-name>DataSourceTestServlet</servlet-name>
        <servlet-class>ServletPackage.DataSourceTestServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>DataSourceTestServlet</servlet-name>
        <url-pattern>/ServletPackage/DataSourceTestServlet</url-pattern>
    </servlet-mapping>
```
## 运行结果
![](/assets/屏幕快照 2018-10-12 上午11.18.52.png)