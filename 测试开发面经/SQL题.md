### 1、给你三个表怎么连接查询
如果有三个表需要进行连接查询，常见的连接方式有内连接（INNER JOIN）、左连接（LEFT JOIN）和右连接（RIGHT JOIN）。

内连接（INNER JOIN）会返回两个表中满足连接条件的行。
```
SELECT * FROM A INNER JOIN B ON A.column1 = B.column1 INNER JOIN C ON A.column2 = C.column2;
```
左连接（LEFT JOIN）会返回左表（即 `LEFT JOIN` 关键字左边的表）中的所有行，以及右表中与左表连接条件匹配的行。如果右表中没有匹配的行，则相应的列值为 `NULL`。
```
SELECT * FROM A LEFT JOIN B ON A.column1 = B.column1 LEFT JOIN C ON A.column2 = C.column2;
```
右连接（RIGHT JOIN）则与左连接相反，它返回右表中的所有行，以及左表中与右表连接条件匹配的行。如果左表中没有匹配的行，则相应的列值为 `NULL`。
```
SELECT * FROM A RIGHT JOIN B ON A.column1 = B.column1 RIGHT JOIN C ON A.column2 = C.column2;
```

`JOIN`（内连接）：
- 只返回两个表中满足连接条件的行的组合。
- 结果集中仅包含在两个表中都存在匹配的行

`FULL JOIN`（全外连接）：
- 返回左表（左外连接）和右表（右外连接）中所有的行。
- 如果在另一个表中没有匹配的行，则对应的值为 `NULL` 。

![[Pasted image 20240801194713.png]]
### 2、查找最受欢迎的老师
假设学生表名为 `students` ，包含列 `student_id` （学生 ID）、`student_name` （学生姓名）。课程表名为 `courses` ，包含列 `course_id` （课程 ID）、`course_name` （课程名称）、`teacher_name` （老师姓名）。选课表名为 `enrolls` ，包含列 `student_id` （学生 ID）、`course_id` （课程 ID）。
以下是可能的 SQL 查询语句来找出受欢迎的老师姓名：
```sql
SELECT t.teacher_name, COUNT(e.student_id) as student_count
FROM courses t
JOIN enrolls e ON t.course_id = e.course_id
GROUP BY t.teacher_name
ORDER BY student_count DESC;
```
### 3、计算员工的奖金
假设有一个名为 `employees` 的表，包含 `employee_id`、`salary` 和 `department` 列。请编写一个 SQL 查询，使用 `CASE WHEN` 语句根据以下规则计算每个员工的奖金：
- 如果员工所在部门是 "销售" 且工资大于 8000，奖金为工资的 20%。
- 如果员工所在部门是 "研发" 且工资大于 10000，奖金为工资的 15%。
- 对于其他部门的员工，如果工资大于 6000，奖金为工资的 10%。
- 否则，奖金为 0 。
```sql
select employee_id,salary,department,
case
	when department='销售' and salary>8000 then salary*0.2
	when department='研发' and salary>10000 then salary*0.15
	when department not in ('销售','研发') and salary>6000 then salary*0.1
	else 0
end as 'award'
from employees
```
#case-when
### 4、找出数学成绩大于 80 分或者英语成绩大于 85 分的学生
有两张表 `students_math` （包含 `student_id` 和 `math_score` 列）和 `students_english` （包含 `student_id` 和 `english_score` 列）
```sql
select student_id from students_math where math_score>80
union
select student_id from students_english where english_score>85
```
#union 合并结果不会有重复行

### 5、计算每天的胜负次数
有一张名为 `matches` 的表，其中包含 `match_date`（比赛日期）和 `result`（比赛结果，例如 'Win' 或 'Loss'）列
```sql
select match_date,
sum(case when result='Win' then 1 else 0 end) as 'win_count',
sum(case when result='Loss' then 1 else 0 end) as 'loss_count',
from match_count
group by match_date
```

### 数据库的索引的优缺点
**数据库索引的优点：**
1. 提高查询速度
    - 能够快速定位到符合查询条件的数据，大大减少了数据检索的时间。例如，在一个包含大量用户信息的表中，如果经常需要根据用户 ID 进行查询，建立索引可以迅速找到对应的用户记录，而无需遍历整个表。
2. 加速表之间的连接
    - 在多表关联操作时，索引可以加快连接的速度，提高数据的合并效率。
3. 确保数据的唯一性
    - 可以用于强制某一列或列组合的唯一性，防止重复数据的插入。

**数据库索引的缺点：**
1. 增加数据插入、更新和删除的时间
    - 因为在这些操作时，数据库需要同时维护索引，导致性能开销增加。比如，向一个有大量索引的大表中插入一条新记录，数据库不仅要插入数据，还要更新所有相关的索引。
2. 占用更多的存储空间
    - 索引需要额外的存储空间来存储索引数据结构。
3. 可能导致查询优化器选择错误的执行计划
    - 在某些复杂的查询中，优化器可能会错误地认为使用索引更高效，而实际上全表扫描可能更快。

综上所述，在数据库设计中，需要根据实际的业务需求和数据访问模式来谨慎地创建索引，以平衡查询性能和数据维护的开销。

### 什么时候使用索引，什么时候不适用索引

**适合使用索引的情况：**
1. 经常用于查询、连接和排序的列
    - 例如，在订单表中，订单号、客户 ID 等经常被用于查询特定订单或关联客户信息的列适合建立索引。
2. 列的值具有高唯一性
    - 像身份证号、电子邮件地址这类唯一性较高的列，建立索引能显著提高查询效率。
3. 经常出现在 WHERE 子句中的列
    - 如果经常根据某列的条件来筛选数据，为其创建索引是有益的。比如在员工表中，经常根据职位来查询员工信息，那么职位列适合建索引。

**不适合使用索引的情况：**
1. 数据量小的表
    - 对于数据量很少的表，全表扫描可能比使用索引更快，因为维护索引的成本可能超过其带来的好处。
2. 频繁更新的列
    - 例如，记录日志的时间戳列，如果频繁更新，创建索引会增加更新操作的开销。
3. 很少用于查询的列
    - 某些列几乎不参与查询操作，为其创建索引是没有必要的。
4. 数据分布不均匀的列
    - 比如一个性别列，只有两种值且分布极不均匀，建立索引可能效果不佳。


总之，在决定是否创建索引时，需要综合考虑数据的操作模式、数据量、列的特点等因素，以达到最佳的性能优化效果。

