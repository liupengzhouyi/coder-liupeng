# JavaWeb 中的监听器

## 算什么东西？

**监听器是一个专门用于对其他对象身上发生的事件或状态改变进行监听和相应处理的对象，当被监视的对象发生情况时，立即采取相应的行动。监听器其实就是一个实现特定接口的普通java程序，这个程序专门用于监听另一个java对象的方法调用或属性改变，当被监听对象发生上述事件后，监听器某个方法立即被执行。**

## 名称解释：

* 事件源:即谁产生的事件
* 事件对象:即产生了什么事件
* 监听器:监听事件源的动作

## 附录

由于事件源可以产生多个动作(即产生多个事件)，而监听器中的每一个方法监听一个动作，故每个监听器中都有很多方法。

## 概念

JavaWeb中的监听器是Servlet规范中定义的一种特殊类，它用于监听web应用程序中的**ServletContext**、**HttpSession**和**ServletRequest**这三大域对象的创建、销毁事件以及监听这些域对象中的属性发生修改的事件。

## 分类

在Servlet规范中定义了多种类型的监听器(一共8个监听器)，它们用于监听的事件源分别为ServletContext，HttpSession和ServletRequest这三个域对象。Servlet规范针对这三个对象上的操作，又把多种类型的监听器划分为三种类型：
* 域对象的生命周期监听:监听域对象自身的创建和销毁。这个监听器需要实现相应的监听器接口:ServletContextListener、HttpSessionListener、ServletRequestListener。
* 域对象的属性监听:监听域对象中属性的增加和删除。这个监听器需要实现的监听器接口为:ServletContextAttributeListener、HttpSessionAttributeListener、ServletRequestAttributeListener
* 感知监听(都与HttpSession域对象有关):监听绑定到HttpSession域中的某个JavaBean对象的状态的监听器。这个监听器需要实现的监听器接口:HttpSessionBindingListener、HttpSessionActiveationListener.


| 类型 | 作用 | 接口 |
| --- | --- | --- |
| 域对象的生命周期监听 | 监听域对象自身的创建和销毁 | ServletContextListener, HttpSessionListener, ServletRequestListener |
| 域对象的属性监听 | 监听域对象中属性的增加和删除 | ServletContextAttributeListener, HttpSessionAttributeListener, ServletRequestAttributeListener|
| 感知监听 | 监听绑定到HttpSession域中的某个JavaBean对象的状态的监听器 | HttpSessionBindingListener, HttpSessionActiveationListener|

## 域对象的生命周期监听

事件源为:三大域事件对象为:创建与销毁监听器为:实现了ServletContextListener、HttpSessionListener、ServletRequestListener这三个接口的监听器

* ServletContext的生命周期监听

    ### Code
    
    ```
    public class AListener implements ServletContextListener{    
        //在项目启动时调用    
        public void contextInitialized(ServletContextEvent sce) {   
        }    
        //在项目关闭时调用    
        public void contextDestroyed(ServletContextEvent sce) {      
        }
    }
    ```
    ### xml文件配置
    
    ```
    <listener>    
        <listener-class>listener.AListener</listener-class>
    </listener>
    ```
    
* HttpSession的生命周期监听

    ### code
    
    ```
    public class AListener implements HttpSessionListener{  
        //在会话产生时调用      
        public void sessionCreated(HttpSessionEvent sce) {      
        }   
         //在会话关闭时调用    
         public void sessionDestroyed(HttpSessionEvent sce) {      
        }
    }
    ```
    
    ### xml文件配置
    
    ```
    <listener>    
        <listener-class>listener.AListener</listener-class>
    </listener>
    ```
    
        


### 附录

* ServletContextEvent类:类中有一个方法getServletContext(),该方法返回ServletContext对象。
* HttpSessionEvent类:类中有一个方法getSession()，该方法返回一个HttpSession对象。
* ServletRequestEvent类:类中有两个方法，getServletContext()用于返回一个ServletContext对象，getServletRequest()用于返回一个ServletRequest对象。



## 域对象的属性监听

事件源:三大域事件对象:属性的增加与删除监听器:实现了ServletContextAttributeListener、HttpSessionAttributeListener、ServletRequestAttributeListener接口的监听器

* ServletContext的属性监听

    ### code
    
       
    ```
     public class AListener implements ServletContextAttributeListener{    
    
        //给ServletContext对象添加属性时调用    
        public void attributeAdded(ServletcontextAttribute scab){      
        }    
        //给ServletContext对象删除属性时调用   
        public void attributeRemoved(ServletContextAttributeEvent scab){    
        }    
        //给ServletContext对象替换属性值时调用    
        public void attributeReplaced(ServletContextAttributeEvent scab){    
        }
    }
    ```
* HttpSession的属性监听

    ### code
    
        
    
        public class AListener implements HttpSessionAttributeListener{   
            //给HttpSession对象添加属性时调用     
            public void attributeAdded(HttpSessionAttribute scab){      
            }    
            //给HttpSession对象删除属性时调用    
            public void attributeRemoved(HttpSessionAttributeEvent   scab){    
            }        
            //给HttpSession对象替换属性值时调用    
            public void attributeReplaced(HttpSessionAttributeEvent                 scab){    
            }
        }
   
        
* ServletRequest的属性监听

    ### code
    
    ```
    public class AListener implements ServletRequestAttributeListener{    
        //给ServletRequest对象添加属性时调用    
        public void attributeAdded(ServletRequestAttribute scab){      
        }    
        //给ServletRequest对象删除属性时调用    
        public void attributeRemoved(ServletRequestAttributeEvent scab){    
        }    
        //给ServletRequest对象替换属性值时调用    
        public void attributeReplaced(ServletRequestAttributeEvent scab){    
        }
    }
    ```

    ### 附录

    ServletContextAttributeEvent类:该类对象有三个方法
    
    * getSevletContext()用于返回一个ServletContext，getName()用于返回属性名，getValue()用于返回属性值。
    
    * HttpSessionBindingEvent类:该类对象有两个方法，getName()用于获取属性名，getValue()用于获取属性值。
    
    * ServletRequestAttributeEvent类:该类对象有两个方法，getName()用于获取属性名，getValue()用于获取属性值。


    
## 感知监听
        

**保存在Session域中的对象可以有多种状态：绑定(session.setAttribute(“bean”,Object))到Session中,随Session对象持久化到一个存储设备中；**

**从Session域中解除(session.removeAttribute(“bean”))绑定,随Session对象从一个存储设备中恢复。**

**Servlet 规范中定义了两个特殊的监听器口”HttpSessionBindingListener和HttpSessionActivationListener”来帮助JavaBean 对象了解自己在Session域中的这些状态，实现这两个接口的类不需要 web.xml 文件中进行注册。**


* HttpSessionBindingListener接口

    ### 简单的概述
    
    实现了HttpSessionBindingListener接口的JavaBean对象可以感   知自己被绑定到Session中和 Session中删除的事件。
    
    当对象被绑定到HttpSession对象中时，web服务器调用该对象的void valueBound(HttpSessionBindingEvent event)方法。
    
    当对象从HttpSession对象中解除绑定时，web服务器调用该对象的void valueUnbound(HttpSessionBindingEvent event)方法。


    ### code
    
    ```
    public class JavaBeanDemo1 implements HttpSessionBindingListener {      
        private String name;  
                
        @Override     
        public void valueBound(HttpSessionBindingEvent event) {         
        System.out.println(name+"被加到session中了");     }      
        
        @Override     
        public void valueUnbound(HttpSessionBindingEvent event) {         
        System.out.println(name+"被session踢出来了");     
        }      
        
        public String getName() {         
        return name;     
        }      
        public void setName(String name) {         
        this.name = name;     
        }      
        public JavaBeanDemo1(String name) {         
        this.name = name;     
        } 
    }
    ```
    
    **上述的JavaBeanDemo1这个javabean实现了HttpSessionBindingListener接口，那么这个JavaBean对象可以感知自己被绑定到Session中和从Session中删除的这两个操作。**    
    
* HttpSessionActivationListener接口

    实现了HttpSessionActivationListener接口的JavaBean对象可以感知自己被活化(反序列化)和钝化(序列化)的事件。
当绑定到HttpSession对象中的javabean对象将要随HttpSession对象被钝化(序列化)之前，web服务器调用该javabean对象的void sessionWillPassivate(HttpSessionEvent event) 方法。这样javabean对象就可以知道自己将要和HttpSession对象一起被序列化(钝化)到硬盘中。
当绑定到HttpSession对象中的javabean对象将要随HttpSession对象被活化(反序列化)之后，web服务器调用该javabean对象的void sessionDidActive(HttpSessionEvent event)方法。这样javabean对象就可以知道自己将要和 HttpSession对象一起被反序列化(活化)回到内存中。(javabean随着HttpSession对象一起被活化的前提是该javabean对象除了实现该接口外还应该实现Serialize接口)。


    ### code
        
    ```
    public class JavaBeanDemo2 implements HttpSessionActivationListener, Serializable {            
        private static final long serialVersionUID = 7589841135210272124L;    
        private String name; 
             
        @Override     
        public void sessionWillPassivate(HttpSessionEvent se) {                  
            System.out.println(name+"和session一起被序列化(钝化)到硬盘了，session的id是："+se.getSession().getId());     
        }      
        @Override     
        public void sessionDidActivate(HttpSessionEvent se) {         
            System.out.println(name+"和session一起从硬盘反序列化(活化)回到内存了，session的id是："+se.getSession().getId());     
        }     
        public String getName() {         
            return name;     
        }     
        public void setName(String name) {         
            this.name = name;     
        }      
        public JavaBeanDemo2(String name) {        
            this.name = name;     
        } 
    }
    ```


