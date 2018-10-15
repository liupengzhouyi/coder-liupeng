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


