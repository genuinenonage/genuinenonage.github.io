# 学习记录
### mongodb  
基于分布式文件存储的数据库。有c++语言编写。旨在为WEB应用提供可扩展的高性能数据存储解决方案。  
### System.currentTimeMillis()  
new Date()所做的事情其实就是调用了System.currentTimeMillis()。
### POJO  
POJO（Plain Ordinary Java Object）简单的Java对象，实际就是普通JavaBeans，是为了避免和EJB混淆所创造的简称。  
POJO实质上可以理解为简单的实体类，顾名思义POJO类的作用是方便程序员使用数据库中的数据表，对于广大的程序员，可以很方便的将POJO类当做对象来进行使用，当然也是可以方便的调用其get,set方法。POJO类也给我们在struts框架中的配置带来了很大的方便。  
### Entity、VO、DTO  
1、entity 里的每一个字段，与数据库相对应，

2、vo 里的每一个字段，是和你前台 html 页面相对应，

3、dto 这是用来转换从 entity 到 vo，或者从 vo 到 entity 的中间的东西 。（DTO中拥有的字段应该是entity中或者是vo中的一个子集）