---
title: mybatis的懒加载与分页查询
date: 2020/08/19 17:21:00
tags:
- mybatis 
- 懒加载
categories:
- spring
---
### 延迟加载  
延迟加载，也叫懒加载，但是懒加载往往与分布查询同时使用  

## 分布查询  
先查询主表，通过主表的道德信息将作为参数传递给关联表，查询关联表的信息。  

	<resultMap id="MystudentStep" type="com.tulun.bean.Student">  
        <id column="id" property="id"></id>  
        <result column="name" property="name"></result>  
        <result column="passward" property="passward"></result>  
        <!--
            association:定义关联对象的封装规则
            select:表明当前属性是调用select 指定的方法查出的结果
            column:指定将哪一列的值传给这个方法
            流程：使用select 指定的方法（传入column 指定的这列参数的值）查出对象，
                    并封装给property 指定的属性
        -->
        <association property="dept"
                     select="com.tulun.dao.DeptMapper.getDeptById"
                     column="d_id">
        </association>
    </resultMap>  


    <select id="getStuByIdStep" resultMap="MystudentStep">
        select * from student where id = #{id}
	</select>
	<select id="getDeptById" resultType="com.tulun.bean.Dept">
     	select * from dept where id = #{id}
	</select>

## 延迟加载  
MyBatis中的延迟加载，也称为懒加载，是指在进行关联查询时，按照设置延迟规则推迟对关联对象的select查询。延迟加载可以有效的减少数据库压力。

Mybatis 根据关联对象查询Select 语句的查询时机分为：直接加载、侵入式加载、深度延迟性加载。  

1. 直接加载  
执行完主加载对象的select语句，马上执行关联对象的Select语句
2. 侵入式加载  
执行完主加载对象查询后不会马上执行关联对象查询，但是当访问主加载对象时，就会加载关联对象的查询。即对关联对象的查询执行，侵入到了主加载对象的详情访问中。也可以这样理解：将关联对象的详情侵入到了主加载对象的详情中，即将关联对象的详情作为主加载对象的详情的一部分出现了。  
3. 深度延迟加载  
执行主对象的查询时不会执行关联对象的执行，访问主对象详情时也不会执行关联对象的查询，只有当访问关联对象时才会对其进行查询 
