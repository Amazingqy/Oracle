### 用户名：qiuyu
### 角色：qqy
### 密码：123


## 为用户分配表空间
<pre><code>ALTER USER qiuyu QUOTA UNLIMITED ON USERS;
ALTER USER qiuyu QUOTA UNLIMITED ON USERS02;
ALTER USER qiuyu QUOTA UNLIMITED ON USERS03;
ALTER USER qiuyu ACCOUNT UNLOCK;</code></pre>

结果：<br>
![](https://github.com/Amazingqy/Oracle/blob/master/test4/%E7%BB%93%E6%9E%9C1.png)

## 为用户分配权限
<pre><code>GRANT "CONNECT" TO qiuyu WITH ADMIN OPTION;
GRANT "RESOURCE" TO qiuyu WITH ADMIN OPTION;
ALTER USER qiuyu DEFAULT ROLE "CONNECT","RESOURCE";</code></pre>
结果：<br>
![](https://github.com/Amazingqy/Oracle/blob/master/test4/%E7%BB%93%E6%9E%9C2.png)

## 系统分配权限
<pre><code>GRANT CREATE VIEW TO xiaoqingyu WITH ADMIN OPTION;</code></pre>
结果：<br>
![](https://github.com/Amazingqy/Oracle/blob/master/test4/%E7%BB%93%E6%9E%9C3.png)
## 表和相应触发器、序列、视图
见test4.sql
## 插入初始化数据
<pre><code>INSERT INTO qiuyu.DEPARTMENTS(DEPARTMENT_ID,DEPARTMENT_NAME) values (1,'总经办');
INSERT INTO qiuyu.EMPLOYEES(EMPLOYEE_ID,NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,SALARY,MANAGER_ID,DEPARTMENT_ID)
  VALUES (1,'李董事长',NULL,NULL,to_date('2010-1-1','yyyy-mm-dd'),50000,NULL,1);
INSERT INTO qiuyu.DEPARTMENTS(DEPARTMENT_ID,DEPARTMENT_NAME) values (11,'销售部1');
INSERT INTO qiuyu.EMPLOYEES(EMPLOYEE_ID,NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,SALARY,MANAGER_ID,DEPARTMENT_ID)
  VALUES (11,'张总',NULL,NULL,to_date('2010-1-1','yyyy-mm-dd'),50000,1,1);
  INSERT INTO qiuyu.EMPLOYEES(EMPLOYEE_ID,NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,SALARY,MANAGER_ID,DEPARTMENT_ID)
  VALUES (111,'吴经理',NULL,NULL,to_date('2010-1-1','yyyy-mm-dd'),50000,11,11);
  INSERT INTO qiuyu.EMPLOYEES(EMPLOYEE_ID,NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,SALARY,MANAGER_ID,DEPARTMENT_ID)
  VALUES (112,'白经理',NULL,NULL,to_date('2010-1-1','yyyy-mm-dd'),50000,11,11);
INSERT INTO qiuyu.DEPARTMENTS(DEPARTMENT_ID,DEPARTMENT_NAME) values (12,'销售部2');
INSERT INTO qiuyu.EMPLOYEES(EMPLOYEE_ID,NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,SALARY,MANAGER_ID,DEPARTMENT_ID)
  VALUES (12,'王总',NULL,NULL,to_date('2010-1-1','yyyy-mm-dd'),50000,1,1);
  INSERT INTO qiuyu.EMPLOYEES(EMPLOYEE_ID,NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,SALARY,MANAGER_ID,DEPARTMENT_ID)
  VALUES (121,'赵经理',NULL,NULL,to_date('2010-1-1','yyyy-mm-dd'),50000,12,12);
  INSERT INTO qiuyu.EMPLOYEES(EMPLOYEE_ID,NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,SALARY,MANAGER_ID,DEPARTMENT_ID)
  VALUES (122,'刘经理',NULL,NULL,to_date('2010-1-1','yyyy-mm-dd'),50000,12,12);

insert into qiuyu.products (product_name,product_type) values ('computer1','电脑');
insert into qiuyu.products (product_name,product_type) values ('computer2','电脑');
insert into qiuyu.products (product_name,product_type) values ('computer3','电脑');
insert into qiuyu.products (product_name,product_type) values ('phone1','手机');
insert into qiuyu.products (product_name,product_type) values ('phone2','手机');
insert into qiuyu.products (product_name,product_type) values ('phone3','手机');
insert into qiuyu.products (product_name,product_type) values ('paper1','耗材');
insert into qiuyu.products (product_name,product_type) values ('paper2','耗材');
insert into qiuyu.products (product_name,product_type) values ('paper3','耗材');
</code></pre>


# 查询数据
## 查询单条数据
<pre><code>--查询数据 id值从10012到20021
select * from qiuyu.ORDERS where  order_id=10012;
select * from qiuyu.ORDER_DETAILS where  order_id=10012;
select * from qiuyu.VIEW_ORDER_DETAILS where order_id=10012;</code></pre>

## 递归查询员工及其下级员工
<pre><code>WITH A (EMPLOYEE_ID,NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,SALARY,MANAGER_ID,DEPARTMENT_ID) AS
  (SELECT EMPLOYEE_ID,NAME,EMAIL,PHONE_NUMBER,HIRE_DATE,SALARY,MANAGER_ID,DEPARTMENT_ID
    FROM qiuyu.employees WHERE employee_ID = 11
    UNION ALL
  SELECT B.EMPLOYEE_ID,B.NAME,B.EMAIL,B.PHONE_NUMBER,B.HIRE_DATE,B.SALARY,B.MANAGER_ID,B.DEPARTMENT_ID
    FROM A, qiuyu.employees B WHERE A.EMPLOYEE_ID = B.MANAGER_ID)SELECT * FROM A;--或SELECT * FROM employees START WITH EMPLOYEE_ID = 11 CONNECT BY PRIOR EMPLOYEE_ID = MANAGER_ID;
</code></pre>
结果：<br>
![](https://github.com/Amazingqy/Oracle/blob/master/test4/%E7%BB%93%E6%9E%9C.png)
