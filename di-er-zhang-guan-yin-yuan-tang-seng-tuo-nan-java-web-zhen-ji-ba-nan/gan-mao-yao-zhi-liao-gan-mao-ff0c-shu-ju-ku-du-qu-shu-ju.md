# 一个课后作业，数据库读取数据
## 功能描述：闲的蛋疼，想找一点事情干。
## 步骤：
### 1.建立一个数据库
#### 代码：
```
create table guestbook
(
  id int primary key auto_increment,
  name varchar(20) not null ,
  phone varchar(20) ,
  email varchar(40) ,
  title varchar(80) not null ,
  content varchar(2000) ,
  time time not null

);

insert into guestbook (id, name, phone, email, title, content, time) value (1, 'liupeng', '14747219744', 'LIUPENG.0@outlook.com', '我的一天', '我看了一天的《喜羊羊与灰太狼》', now());

select * from guestbook;
```
### 2.JavaBean做数据库连接类
#### 代码：
```
package JavaBean.linkDatabase;

import java.sql.*;

public class linkDatabases {
    // JDBC 驱动名及数据库 URL
    static final String JDBC_DRIVER = "com.mysql.jdbc.Driver";
    static final String DB_URL = "jdbc:mysql://localhost:3306/database_for_java_web";
    // 数据库的用户名与密码，需要根据自己的设置
    static final String USERNAME = "root";
    static final String PASSWORD = "lp184126";

    private Connection connection = null;

    private Statement statement = null;

    public linkDatabases() throws ClassNotFoundException {
        Class.forName(JDBC_DRIVER);
    }

    public void createConnection() throws SQLException {
        connection = DriverManager.getConnection(
                DB_URL,
                USERNAME,
                PASSWORD
        );
    }

    public Connection getConnection() throws SQLException {
        this.createConnection();
        if (connection == null) {
            this.createConnection();
            return connection;
        } else {
            return connection;
        }
    }

    public void createStatement() throws SQLException {
        if (this.statement != null) {
            return;
        } else {
            if (this.getConnection() == null) {
                this.createConnection();
            } else {
                this.statement = this.getConnection().createStatement();
            }
        }
    }

    public Statement getStatement() throws SQLException {
        if (this.connection == null) {
            this.createStatement();
        } else {
            this.statement = this.getConnection().createStatement();
        }
        return this.statement;
    }

    public boolean saveData(String str) throws SQLException {
        this.createConnection();
        this.createStatement();
        if (this.statement == null) {
            return false;
        } else {
            String string = str;
            //string = "INSERT INTO user (lp_id, lp_name, lp_password) VALUES (1809120006,1234,1234);";
            this.statement.execute(string);
            return true;
        }
    }

    public ResultSet getInformation(String sql) throws SQLException {
        this.createConnection();
        this.createStatement();
        // System.out.print(sql);
        ResultSet resultSet = this.statement.executeQuery(sql);
        return resultSet;
    }

/*
    public static void main(String[] args) throws SQLException, ClassNotFoundException {
        linkDatabases linkDatabase = new linkDatabases();
        // linkDatabase.saveData("insert into lp_sleep_table(lp_id, lp_date, lp_time1) value (2, '2018-09-27', '21:58:32');");
        *//*Connection connection = linkDatabase.getConnection();
        if (connection != null) {
            System.out.print("数据库链接成功！！");
            String string = "INSERT INTO user (lp_id, lp_name, lp_password) VALUES (1809120007,1234,1234);";
            boolean ifSave = linkDatabase.saveData(string);
            if (ifSave) {
                System.out.print("数据保存成功！");
            } else {
                System.out.print("数据没有保存！");
            }
        } else {
            System.out.print("数据库链接失败！");
        }*//*
    }*/
}

```
### 3.from表单提交数据
#### 代码：
```
<%--
  Created by IntelliJ IDEA.
  User: liupeng
  Date: 2018/10/8
  Time: 1:00 PM
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<form method="post" action="ServletPackage/work2Servlet">
    姓名：
    <input type="text" name="name" value=""><br>
    电话：
    <input type="text" name="phone" value=""><br>
    Email：
    <input type="text" name="email" value=""><br>
    主题：
    <input type="text" name="title" value=""><br>
    内容：
    <input type="text" name="content" value=""><br>
    <input type="reset" value="重置">&nbsp;&nbsp;
    <input type="submit" value="提交">
</form>

</body>
</html>

```
### 4.servlet抓去数据，存储
#### 代码：
```
package ServletPackage;

import JavaBean.Test.getNowTime;
import JavaBean.linkDatabase.getSQLString;
import JavaBean.linkDatabase.linkDatabases;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.sql.SQLException;

@WebServlet(name = "work2Servlet")
public class work2Servlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");
        PrintWriter out=response.getWriter();
        String l_name=request.getParameter("name");
        String l_phone=request.getParameter("phone");
        String l_email=request.getParameter("email");
        String l_title=request.getParameter("title");
        String l_content=request.getParameter("content");
        out.print("<table border=2>");
        out.print("<tr>");
        out.print("<td>姓名</td>");
        out.print("<td>"+l_name+"</td>");
        out.print("<td>电话</td>");
        out.print("<td>"+l_phone+"</td>");
        out.print("<td>Email</td>");
        out.print("<td>"+l_email+"</td>");
        out.print("<td>题目</td>");
        out.print("<td>"+l_title+"</td>");
        out.print("<td>内容</td>");
        out.print("<td>"+l_content+"</td>");
        try {
            String l_time = new getNowTime().getTime();
            getSQLString lpgetSQLString = new getSQLString();
            lpgetSQLString.setSqlForWord2_1(l_name, l_phone, l_email, l_title, l_content, l_time);
            String sql = lpgetSQLString.getSqlForWord2_1();
            linkDatabases lpLinkDatabases = new linkDatabases();
            boolean key = lpLinkDatabases.saveData(sql);
            if (key) {
                out.print("数据保存成功！");
            } else {
                out.print("数据保存失败！");
            }
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}

```
### 5.servlet获取数据，显示
#### 代码：
```
package ServletPackage;

import JavaBean.linkDatabase.getSQLString;
import JavaBean.linkDatabase.linkDatabases;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;
import java.sql.ResultSet;
import java.sql.SQLException;

@WebServlet(name = "work2getInformationServlet")
public class work2getInformationServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        request.setCharacterEncoding("utf-8");
        response.setContentType("text/html;charset=utf-8");
        PrintWriter out = response.getWriter();

        getSQLString lpGetSQLString = new getSQLString();
        lpGetSQLString.setSqlForWord2_2();
        String sql = lpGetSQLString.getSqlForWord2_2();
        try {
            out.print("<table>");
            linkDatabases lpLinkDatabases = new linkDatabases();
            ResultSet resultSet = lpLinkDatabases.getInformation(sql);
            while(resultSet.next()) {
                String name = resultSet.getString("name");
                String phone = resultSet.getString("phone");
                String email = resultSet.getString("email");
                String title = resultSet.getString("title");
                String content = resultSet.getString("content");
                String time = resultSet.getString("time");

                out.print("<tr>");
                out.print("<td>姓名</td>");
                out.print("<td>"+name+"</td>");
                out.print("<td>电话</td>");
                out.print("<td>"+phone+"</td>");
                out.print("<td>Email</td>");
                out.print("<td>"+email+"</td>");
                out.print("<td>题目</td>");
                out.print("<td>"+title+"</td>");
                out.print("<td>内容</td>");
                out.print("<td>"+content+"</td>");
                out.print("<td>时间</td>");
                out.print("<td>"+time+"</td>");
                out.print("</tr>");
            }
            out.print("</table>");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}

```
## 效果：
### 获取数据表单
![](/assets/屏幕快照 2018-10-15 上午9.01.11.png)
### 提交数据表单
![](/assets/屏幕快照 2018-10-15 上午9.01.35.png)
### 获取数据表单
![](/assets/屏幕快照 2018-10-15 上午9.02.12.png)
