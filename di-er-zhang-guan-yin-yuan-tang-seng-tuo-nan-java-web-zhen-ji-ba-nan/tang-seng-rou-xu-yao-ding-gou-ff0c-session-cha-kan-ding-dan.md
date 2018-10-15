# Session 查看订单
## 需求分析：
**唐僧肉一斤难求，骗子马云在网上某宝贩卖唐僧肉，帅气十足的刘鹏订购了一斤，可是这骗子马云的某宝把订单丢了，我需要重新实现某宝的订单查看功能。**
## 实现步骤
![](/assets/屏幕快照 2018-10-15 下午3.18.56.png)
## 创建Session

## 销毁Session

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


