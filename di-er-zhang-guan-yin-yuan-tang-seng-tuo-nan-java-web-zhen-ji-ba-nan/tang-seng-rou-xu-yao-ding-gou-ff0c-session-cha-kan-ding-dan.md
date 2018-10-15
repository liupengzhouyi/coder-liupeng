# Session 查看订单

## 需求分析：

**唐僧肉一斤难求，骗子马云在网上某宝贩卖唐僧肉，帅气十足的刘鹏订购了一斤，可是这骗子马云的某宝把订单丢了，我需要重新实现某宝的订单查看功能。**

## 实现步骤

![](/assets/屏幕快照 2018-10-15 下午3.18.56.png)

## 创建Session

```
package Session;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;
import java.io.PrintWriter;

@WebServlet(name = "Session01Servlet")
public class Session01Servlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        response.setContentType("text/html; charset=UTF-8");

        //使用request对象的getSession()获取session，如果session不存在则创建一个
        HttpSession session = request.getSession();

        //获取session的Id
        String sessionId = session.getId();

        //判断session是不是新创建的
        if (session.isNew()) {
            response.getWriter().print("session创建成功，session的id是："+sessionId);
            session.setAttribute("name","123");
        }else {
            response.getWriter().print("服务器已经存在session，session的id是：" + sessionId + "  " + session.getAttribute("name"));

        }




    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}
```

## 销毁Session

```
package Session;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;

@WebServlet(name = "DeleteSessionServlet")
public class DeleteSessionServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //获取session
        HttpSession session = request.getSession();
        //获取数据
        String name = (String) session.getAttribute("name");
        //打印数据
        System.out.print(name);
        //销毁session
        session.invalidate();
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }
}
```

## 数据库

```
create table lp_uesr_table_for_java_web
(
  user_id int primary key auto_increment,
  user_name varchar(20) not null ,
  user_password varchar(30) not null
);

create table lp_goods_for_java_web
(
  good_id int primary key auto_increment,
  good_name varchar(20) not null ,
  good_prich float
);


create table lp_shop_book_for_java_web
(
  book_id int primary key auto_increment,
  user_id int not null ,
  good_id int not null ,
  number int not null ,
  book_date datetime not null
);
```

## 情况：有用户登录与用户注册的分流

### 代码

```
<%--
  Created by IntelliJ IDEA.
  User: liupeng
  Date: 2018/10/15
  Time: 3:58 PM
  To change this template use File | Settings | File Templates.
--%>

<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>登录</title>
</head>
<body>
    <p>1</p><a href="login.jsp"><button>登录</button></a>
    <p>2</p><a href="sign_in.jsp"><button>注册</button></a>
</body>
</html>
```

### 登录代码

```
<%--
  Created by IntelliJ IDEA.
  User: liupeng
  Date: 2018/10/15
  Time: 3:56 PM
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>登录</title>
</head>
<body>
    <form action="/Session/LogInServlet_for_Java_web" method="post">
        <p>用户ID</p><input type="text" name="user_id"><br>
        <p>密码&nbsp;&nbsp;</p><input type="password" name="user_password"><br>
        <input type="reset" value="重置">&nbsp;&nbsp;&nbsp;
        <input type="submit" value="提交">
    </form>
</body>
</html>
```

### 注册代码

```
<%--
  Created by IntelliJ IDEA.
  User: liupeng
  Date: 2018/10/15
  Time: 3:56 PM
  To change this template use File | Settings | File Templates.
--%>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
<head>
    <title>登录</title>
</head>
<body>
    <form action="/Session/LogInServlet_for_Java_web" method="post">
        <p>用户ID</p><input type="text" name="user_id"><br>
        <p>密码&nbsp;&nbsp;</p><input type="password" name="user_password"><br>
        <input type="reset" value="重置">&nbsp;&nbsp;&nbsp;
        <input type="submit" value="提交">
    </form>
</body>
</html>
```

### 注册代码中的servlet


```
package Session;

import JavaBean.linkDatabase.getSQLString;
import JavaBean.linkDatabase.linkDBByDBCP;

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

@WebServlet(name = "getInformationServlet_forJava_web")
public class getInformationServlet_forJava_web extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String user_name = request.getParameter("user_name");
        String user_passwordI = request.getParameter("user_passwordI");
        String user_passwordII = request.getParameter("user_passwordII");

        response.setContentType("text/html; charset=UTF-8");

        if (user_name.isEmpty() || user_passwordI.isEmpty() || user_passwordII.isEmpty()) {
            //没有完全的输入
            this.donotinput(request, response);
        } else if(user_passwordI.equals(user_passwordII)) {
            //可以注册
            try {
                this.saveUser(user_name, user_passwordI, request, response);
            } catch (NamingException e) {
                e.printStackTrace();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        } else {
            //密码不一样
            this.diffPassword(request, response);
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }

    //没有完全的输入
    public void donotinput(HttpServletRequest request, HttpServletResponse response) throws IOException {
        PrintWriter out = response.getWriter();
        out.print("" +
                "<h1>\n" +
                "        <center>\n" +
                "            有未输入的数据，请重新设置\n" +
                "        </center>\n" +
                "    </h1>");
        out.print("<form action=\"/Session/getInformationServlet_forJava_web\" method=\"post\">\n" +
                "        <p>请输入用户名：</p><input type=\"text\" name=\"user_name\">\n" +
                "        <p>请输入密码：</p><input type=\"password\" name=\"user_passwordI\">\n" +
                "        <p>请再次输入密码：</p><input type=\"password\" name=\"user_passwordII\">\n" +
                "        <input type=\"reset\" value=\"重置\">\n" +
                "        <input type=\"submit\" value=\"提交\">\n" +
                "    </form>");
    }

    //密码不一样
    public void diffPassword(HttpServletRequest request, HttpServletResponse response) throws IOException {
        PrintWriter out = response.getWriter();
        out.print("" +
                "<h1>\n" +
                "        <center>\n" +
                "            密码不一致，请重新设置\n" +
                "        </center>\n" +
                "    </h1>");
        out.print("<form action=\"/Session/getInformationServlet_forJava_web\" method=\"post\">\n" +
                "        <p>请输入用户名：</p><input type=\"text\" name=\"user_name\">\n" +
                "        <p>请输入密码：</p><input type=\"password\" name=\"user_passwordI\">\n" +
                "        <p>请再次输入密码：</p><input type=\"password\" name=\"user_passwordII\">\n" +
                "        <input type=\"reset\" value=\"重置\">\n" +
                "        <input type=\"submit\" value=\"提交\">\n" +
                "    </form>");
    }

    public void saveUser(String name, String passowrd, HttpServletRequest request, HttpServletResponse response) throws NamingException, SQLException, IOException {

        //获取SQL语句
        getSQLString lpGetSQLString = new getSQLString();
        lpGetSQLString.setSql11(name, passowrd);
        String sql = lpGetSQLString.getSql11();
        //获取数据库存储类
        linkDBByDBCP lpLinkDBByDBCP = new linkDBByDBCP();
        if (lpLinkDBByDBCP != null) {
            lpLinkDBByDBCP.saveData(sql);
        }



        PrintWriter out = response.getWriter();
        out.print("" +
                "<h1>\n" +
                "        <center>\n" +
                "            注册完成\n" +
                "        </center>\n" +
                "</h1>");
    }

}
```


### 登录代码中的Servlet


```
package Session;

import JavaBean.linkDatabase.getSQLString;
import JavaBean.linkDatabase.linkDBByDBCP;

import javax.naming.NamingException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;
import java.io.PrintWriter;
import java.sql.ResultSet;
import java.sql.SQLException;

@WebServlet(name = "LogInServlet_for_Java_web")
public class LogInServlet_for_Java_web extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String id = request.getParameter("user_id");
        String password = request.getParameter("user_password");
        String password_in_database = null;

        response.setContentType("text/html; charset=UTF-8");

        try {
            ResultSet resultSet = this.getInformation(id);
            while(resultSet.next()){
                password_in_database = resultSet.getString("user_password");
            }
            if (password_in_database.equals(password)) {
                //登录成功
                this.createSession(request, response, id);
            } else {
                //密码错误
                this.errorPassWord(request, response);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        } catch (NamingException e) {
            e.printStackTrace();
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }

    public ResultSet getInformation(String id) throws SQLException, NamingException {
        ResultSet resultSet = null;

        //获取SQL语句
        getSQLString lpGetSQLString = new getSQLString();
        lpGetSQLString.setSql12(id);
        String sql = lpGetSQLString.getSql12();

        //获取SQL语句
        linkDBByDBCP lpLinkDBByDBCP = new linkDBByDBCP();
        if (lpLinkDBByDBCP != null) {
            resultSet = lpLinkDBByDBCP.getData(sql);
        }

        return resultSet;
    }

    //密码错误
    public void errorPassWord(HttpServletRequest request, HttpServletResponse response) throws IOException {
        PrintWriter out = response.getWriter();
        out.print("" +
                "<h1>\n" +
                "        <center>\n" +
                "            密码错误\n" +
                "        </center>\n" +
                "    </h1>");
        out.print("<form action=\"\" method=\"post\">\n" +
                "        <p>用户ID</p><input type=\"text\" name=\"user_id\"></form><br>\n" +
                "        <p>密码&nbsp;&nbsp;</p><input type=\"password\" name=\"user_password\"><br>\n" +
                "        <input type=\"reset\" value=\"重置\">&nbsp;&nbsp;&nbsp;\n" +
                "        <input type=\"submit\" value=\"提交\">\n" +
                "    </form>");
    }

    //登录成功，创建Session
    public void createSession(HttpServletRequest request, HttpServletResponse response, String id) throws IOException {
        //使用request对象的getSession()获取session，如果session不存在则创建一个
        HttpSession sessionI = request.getSession();
        sessionI.invalidate();

        HttpSession session = request.getSession();
        //获取session的Id
        String sessionId = session.getId();

        //判断session是不是新创建的
        if (session.isNew()) {
            response.getWriter().print("session创建成功，session的id是："+sessionId);
            session.setAttribute("user_id",id);
        }else {
            response.getWriter().print("服务器已经存在session，session的id是：" + sessionId + "  " + session.getAttribute("user_id"));
        }
        response.getWriter().print("<a href=\"127.0.0.1/test/Test_for_Tang/showShop.jsp\" >跳转到订单添加！</a>");
    }
}
```
### 逻辑结构
![](/assets/屏幕快照 2018-10-15 下午7.48.02.png)

## 添加订单的Servlet
```
package Session;
// C9TL3
import JavaBean.Test.getNowTime;
import JavaBean.linkDatabase.getSQLString;
import JavaBean.linkDatabase.linkDBByDBCP;

import javax.naming.NamingException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;
import java.io.PrintWriter;
import java.sql.ResultSet;
import java.sql.SQLException;

@WebServlet(name = "getOrderServlet")
public class getOrderServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=UTF-8");
        //获取提交表单
        String goodName = request.getParameter("name");
        String number = request.getParameter("number");
        //获取用户
        String user_id = null;
        String user_name = null;
        // 获取Session
        HttpSession session = request.getSession();
        user_id = (String) session.getAttribute("user_id");
        // 整合数据
        try {
            this.doFuck(request, response, goodName, number, user_id, user_name);
        } catch (SQLException e) {
            e.printStackTrace();
        } catch (NamingException e) {
            e.printStackTrace();
        }
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        doPost(request, response);
    }

    // 整合数据
    public void doFuck(HttpServletRequest request, HttpServletResponse response, String goodName, String number, String
            user_id, String user_name) throws SQLException, NamingException, IOException {
        //获取SQL语句
        getSQLString lpGetSQLString = new getSQLString();
        //通过用户ID获取用户名
        lpGetSQLString.setSql15(user_id);
        String sqlGetUserName = lpGetSQLString.getSql15();
        //通过货物名称获取货物的ID
        lpGetSQLString.setSql16(goodName);
        String sqlGetGoodId = lpGetSQLString.getSql16();
        ResultSet resultSet = null;

        String name = null;
        String goodId = null;
        int goodPrice = 0;
        //获取数据库存储类
        linkDBByDBCP lpLinkDBByDBCP = new linkDBByDBCP();
        if (lpLinkDBByDBCP != null) {
            resultSet = lpLinkDBByDBCP.getData(sqlGetUserName);
            while (resultSet.next()) {
                name = resultSet.getString("user_name");
            }
        }
        if (lpLinkDBByDBCP != null) {
            resultSet = lpLinkDBByDBCP.getData(sqlGetGoodId);
            while (resultSet.next()) {
                goodId = resultSet.getString("good_id");
                goodPrice = resultSet.getInt("good_prich");
            }
        }



        //获取总价
        int price = Integer.parseInt(number) * goodPrice;

        //获取当前时间
        getNowTime lpGetNowTime = new getNowTime();
        String datetime = lpGetNowTime.getDateTime();

        PrintWriter out = response.getWriter();

        out.print("" +
                "<form action=\"/Session/SaveOrderServlet\" method=\"post\">" +
                "        <table border=\"1\">\n" +
                "            <tr>\n" +
                "                <th>\n" +
                "                    订单属性\n" +
                "                </th>\n" +
                "                <th>\n" +
                "                    您的选择\n" +
                "                </th>\n" +
                "            </tr>\n" +
                "            <tr>\n" +
                "                <th>\n" +
                "                    商品编号\n" +
                "                </th>\n" +
                "                <td>\n" +
                goodId +
                "                </td>\n" +
                "            </tr>\n" +
                "            <tr>\n" +
                "                <th>\n" +
                "                    商品名称\n" +
                "                </th>\n" +
                "                <td>\n" +
                goodName +
                "                </td>\n" +
                "            </tr>\n" +
                "            <tr>\n" +
                "                <th>\n" +
                "                    用户编号\n" +
                "                </th>\n" +
                "                <td>\n" +
                user_id +
                "                </td>\n" +
                "            </tr>\n" +
                "            <tr>\n" +
                "                <th>\n" +
                "                    用户名称\n" +
                "                </th>\n" +
                "                <td>\n" +
                name +
                "                </td>\n" +
                "            </tr>\n" +
                "            <tr>\n" +
                "                <th>\n" +
                "                    商品单价\n" +
                "                </th>\n" +
                "                <td>\n" +
                goodPrice +
                "                </td>\n" +
                "            </tr>\n" +
                "            <tr>\n" +
                "                <th>\n" +
                "                    商品数量\n" +
                "                </th>\n" +
                "                <td>\n" +
                number +
                "                </td>\n" +
                "            </tr>\n" +
                "            <tr>\n" +
                "                <th>\n" +
                "                    总价\n" +
                "                </th>\n" +
                "                <td>\n" +
                price  +
                "                </td>\n" +
                "            </tr>\n" +
                "            <tr>\n" +
                "                <th>\n" +
                "                    下单时间\n" +
                "                </th>\n" +
                "                <td>\n" +
                datetime +
                "                </td>\n" +
                "            </tr>\n" +
                "    </form>");

        //保存数据
        if (lpLinkDBByDBCP != null) {
            lpGetSQLString.setSql17(user_id,goodId,number,datetime);
            String sql = lpGetSQLString.getSql17();
            lpLinkDBByDBCP.saveData(sql);
        }

    }
}

```

## 用户获取自己的订单
```
package Session;

import JavaBean.linkDatabase.getSQLString;
import JavaBean.linkDatabase.linkDBByDBCP;

import javax.naming.NamingException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.io.IOException;
import java.io.PrintWriter;
import java.sql.ResultSet;
import java.sql.SQLException;

@WebServlet(name = "SaveOrderServlet")
public class SaveOrderServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        HttpSession httpSession = request.getSession();
        String userId = (String) httpSession.getAttribute("user_id");
        getSQLString lpgetSQLString = new getSQLString();
        lpgetSQLString.setSql19(userId);
        String sql = lpgetSQLString.getSql19();
        ResultSet resultSet = null;
        response.setContentType("text/html;charset=UTF-8");
        PrintWriter out = response.getWriter();
        out.print("" +
                "<table>\n" +
                "        <tr>\n" +
                "            <th>\n" +
                "                订单号\n" +
                "            </th>\n" +
                "            <th>\n" +
                "                用户名\n" +
                "            </th>\n" +
                "            <th>\n" +
                "                商品名称\n" +
                "            </th>\n" +
                "            <th>\n" +
                "                数量\n" +
                "            </th>\n" +
                "            <th>\n" +
                "                订单时间\n" +
                "            </th>\n" +
                "        </tr>");
        try {
            linkDBByDBCP lpLinkDBByDBCP = new linkDBByDBCP();
            resultSet = lpLinkDBByDBCP.getData(sql);
            while (resultSet.next()) {
                int book_id = resultSet.getInt("订单号");
                String user_name = resultSet.getString("用户名");
                String good_name = resultSet.getString("商品名");
                int number = resultSet.getInt("数量");
                String date = resultSet.getString("订单日期");
                out.print("" +
                        "<tr>\n" +
                        "            <th>\n" +
                        book_id +
                        "            </th>\n" +
                        "            <th>\n" +
                        user_name +
                        "            </th>\n" +
                        "            <th>\n" +
                        good_name +
                        "            </th>\n" +
                        "            <th>\n" +
                        number +
                        "            </th>\n" +
                        "            <th>\n" +
                        date +
                        "            </th>\n" +
                        "        </tr>");
            }
            out.print("</table>");
        } catch (NamingException e) {
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
### 效果图片
![](/assets/屏幕快照 2018-10-15 下午11.29.48.png)

**这就算是完成了吧！但是有一些Bug，会出现404，因为路径的问题，就不修改了，文章中用到了几个JavaBean，代码在GitHub上，项目名Snowman**

# 





























