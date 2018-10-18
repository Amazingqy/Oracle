# 实验一：分析SQL执行计划，执行SQL语句的优化指导
## 实验内容：
1.对Oracle12c中的HR人力资源管理系统中的表进行查询与分析。</br>
2.首先运行和分析教材中的样例：本训练任务目的是查询两个部门('IT'和'Sales')的部门总人数和平均工资，以下两个查询的结果是一样的。但效率不相同。</br>
3.设计自己的查询语句，并作相应的分析，查询语句不能太简单。</br></br></br></br>



### 内容一：对Oracle12c中的HR人力资源管理系统中的表进行查询与分析。
#### 查询1实行及结果
![a](https://github.com/Amazingqy/Oracle/blob/master/tree/master/test1/a.png)
优化指导：要给数据库创建索引来改进执行计划
#### 查询2实行及结果
![c](https://github.com/Amazingqy/Oracle/blob/master/tree/master/test1/c.png)
优化指导：无优化指导
#### 分析比较：
分析：查询1的查询速度比查询2的速度快的多，但是查询1太过单调，没有详细的内容，只有结果。而查询2就十分直观，有详细的内容，但是速度相对慢很多。




### 内容二：设计自己的查询语句，并作相应的分析，查询语句不能太简单。

各个部门平均、最大、最小工资、人数，按照部门号升序排列
![e](https://github.com/Amazingqy/Oracle/blob/master/tree/master/test1/e.png)
分析：职员表中，查询出工资的的数目然后算出平均值，然后按照ID来排序
