# 页面重定向

## java重定向分三种：

1. 相对路径
2. 绝对路径
3. 其他web应用地址

## 函数代码：

| 重定向种类 | 代码 |
| :--- | :--- |
| 相对路径 | response.sendRedirect\("Manager/index.jsp"\); |
| 绝对路径 | response.sendRedirect\("/Manager/index.jsp"\); |
| 其他网站路径 | response.sendRedirect\("[http://cn.bing.com"\](http://cn.bing.com"\)\); |



