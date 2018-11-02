### 创建角色和用户
用户：qiuyu</br>
角色：qy</br>
密码:123</br></br></br></br>

#### 第一步：
以system登录到pdborcl，创建角色qy和用户qiuyu ，并进行授权和分配空间</br>
<pre><code>$ sqlplus system/123@pdborcl
SQL> CREATE ROLE con_res_view;
Role created.
SQL> GRANT connect,resource,CREATE VIEW TO qy;
Grant succeeded.
SQL> CREATE USER qiuyu IDENTIFIED BY 123 DEFAULT TABLESPACE users TEMPORARY TABLESPACE temp;
User created.
SQL> ALTER USER qiuyu QUOTA 50M ON users;
User altered.
SQL> GRANT qy TO new_user;
Grant succeeded.
SQL> exit</pre></code>




#### 第二步:
使用新用户连接到pdborcl，创建表mytable和视图myview，插入数据，最后将myview的SELECT对象权限授予hr用户</br>

<pre><code>$ sqlplus qiuyu/123@pdborcl
SQL> show user;
USER is "NEW_USER"
SQL> CREATE TABLE mytable (id number,name varchar(50));
Table created.</br>
SQL> INSERT INTO mytable(id,name)VALUES(1,'zhang');
1 row created.</br>
SQL> INSERT INTO mytable(id,name)VALUES (2,'wang');
1 row created.</br>
SQL> INSERT INTO mytable(id,name)VALUES (3,'xiao');
1 row created.</br>
SQL> CREATE VIEW myview AS SELECT name FROM mytable;
View created.
SQL> SELECT * FROM myview;
NAME
--------------------------------------------------
zhang
wang
xiao
SQL> GRANT SELECT ON myview TO hr;
Grant succeeded.
SQL>exit
</pre></code>
#### 第三步：
用户hr连接到pdborcl，查询新用户授予它的视图myview
<pre><code>$ sqlplus hr/123@pdborcl
SQL> SELECT * FROM xiaoqingyu.myview;
NAME
--------------------------------------------------
zhang
wang
xiao
SQL> exit</pre></code>

#### 第四步:
测试并分享




