## SQL查询语言

#### 建立关系模式

- CREAT TABLE <关系名>

​		(<属性名> <属性类型>[NOT NULL]，...，

​				完整性约束1，完整性约束2，...)

- 属性类型
- 完整性约束

#### 修改关系模式

> 在一个关系中增加或者删除一个属性

- ALTER TABLE <关系名> ADD|DROP <列名><列类型>

#### 删除关系模式

> 删除一个关系

- DROP TABLE <关系名>

#### 建立索引

#### 删除索引

> 删除索引

- DROP INDEX <索引名>

#### 授权

> 向用户授予操纵数据库对象的权限

- GRANT <pribilege list> ON <object> TO <user ID list>

​		[WITH GRANT OPTION]

**pribilege list**：权限列表

**object**：关系

**user ID list**：用户列表

例如：

​	*把关系R上的SELECT权限赋予用户user*

```sql
GRANT select
ON 	  R
TO    user;
```

#### 权限收回

> 撤销用户在数据库上的操作权限

- REVOKE<pribilege list> ON <object> FROM <user ID list>

​	   [WITH REVOKE OPTION]

## SQL查询

#### 单表查询

> 查询涉及一个表

- **选择表中若干列**

  > 属于投影操作
  >
  > 主要是SELECT部分后面的内容

  SELECT <列表达式>

  FROM 表名

  - **查询指定列**

    <列名1，列名2，...>

  - **查询全部列**

    <*>

  - **查询经过计算的值**

    列名为表达式

    - 算数表达式
  
    例：2022 - 列名1
  
    - 字符串常量
    - 函数
  
  - **使用列别名**
  
    ```sql
    SELECT Sname NAME，2013-Sage BIRTHDAY，
    		LOWER(Sdept) DEPARTMENT
    FROM Student；
    ```
  
    - LOWER()
    
      将属性值改为小写
    
    - UPPER()
    
      将属性值改为大写
    
    - TRIM()
    
      去掉属性值前后的空格

- **选择表中若干元组**

  > 属于选择操作
  >
  > 主要是WHERE子句后面的内容

  - **消除取值重复的行**

    - DISTINCT(作用范围是所有目标列)

  - **不消除重复的行**

    - ALL

  - **常用的查询条件**

    | 查询条件 | 谓词                                                         |
    | -------- | ------------------------------------------------------------ |
    | 比较     | =，>，<，>=，<=，<>                                          |
    | 确定范围 | BETWEEN  AND，NOT  BETWEEN AND                               |
    | 确定集合 | IN，NOT  IN                                                  |
    | 字符匹配 | LIKE，NOT  LIKE                            通配符**%**代替0/n个字符，**_**仅代替1个字符 |
    | 空值     | IS  NULL，IS  NOT  NULL                                      |
    | 多重条件 | AND，OR                                                      |

    > **ESCAPE** 短语：当查询字符串本身含有**%**或**_**时，使用**ESCATE** **'%或_'** 对通配符进行转义。
    >
    > ![image-20230308105554287](C:\Users\ANG\AppData\Roaming\Typora\typora-user-images\image-20230308105554287.png)

  - **对查询结果进行排序**

    - 使用ORDER DY子句

      - 按一个或多个属性列排序

      - 升序：ASC；降序：DESC；省缺为升序；空值元组最后显示

        > ![image-20230308110501904](C:\Users\ANG\AppData\Roaming\Typora\typora-user-images\image-20230308110501904.png)

- 聚集函数

  - 统计元组个数

    COUNT (*)

  - 统计列中值的属性

    | 作用                 | 语句         |
    | -------------------- | ------------ |
    | 一列中值的个**数**   | COUNT (列名) |
    | 一列中值的**总和**   | SUM (列名)   |
    | 一列中值的**平均值** | AVG (列名)   |
    | 一列中值的**最大值** | MAX (列名)   |
    | 一列中值的**最小值** | MIN (列名)   |

    > **DISTINCT**：不统计重复
    >
    > **ALL**：统计所有
    >
    > ![image-20230308111818306](C:\Users\ANG\AppData\Roaming\Typora\typora-user-images\image-20230308111818306.png)

- **分组聚集**

  - 使用**GROUP** **BY** 子句分组

    - 按指定的一列或多列值分组，值相等的为一组
    - 使用GROUP BY 子句，SELECT 子句的列名中只能出现**分组属性**和**聚集函数**。
    - GROUP BY 子句作用的对象是查询的**中间结果**表（GROUP BY查询结果不是用于输出）。

    > HAVING 短语筛选最终输出结果。
    >
    > - WHERE 子句筛选满足条件的**元组**。
    > - HAVING 短语作用于分组，从中选择满足条件的**分组**。

#### 连接查询

> 同时涉及多个表的查询称为连接查询。
>
> 连接条件中的各连接属性类型必须是可比的，但不必是相同的。

- 广义笛卡尔积

  SELECT * FROM R，S；输出结果是表R，S的笛卡尔积。

- ʘ连接

  - 在关系的笛卡尔积上使用连接条件 **WHERE** 产生结果。

    > FROM 子句中包括多个关系。
    >
    > WHERE 子句中包括连接多个表的条件。

  - JOIN ON 表示方法

    > R JOIN S ON <连接条件>

- 自然连接

  在等值连接中把目标列中重复的属性去掉

  - NATURAL JOIN 关键字

    > Select *
    >
    > From Student NATURAL JOIN SC;

  - JOIN USING 关键字

    - 指定属性进行自然连接

      > Select *
      >
      > From R JOIN S USING(A1,A2...);

- 自连接

  一个表与其自己进行连接。

  - 需要给表起别名来区分
  - 属性必须使用别名前缀

- 外连接

  > 保留关系中未通过连接匹配的元组

  - R LEFT/RIGHT/FULL OUTER JOIN S ON 连接条件
  - R NATURAL LEFT/RIGHT/FULL OUTER JOIN S ON 连接条件 USING (A1, A2...);

#### 嵌套查询

> 一个SELECT-FROM-WHERE语句称为一个查询块
>
> 一个查询嵌套在另一个查询块的**WHERE**子句或**HAVING**短语中称为嵌套查询
>
> 嵌套查询由里向外处理
>
> 子查询不能使用**ORDER BY**子句

- 不相关子查询
  - 子查询条件不依赖于父查询，由里向外逐层处理。
- 相关子查询
  - 逐个取外层查询中的元组，取该元组属性参与内查询，若WHERE子句返回值为真，则将此元组放入结果表。

- 子查询中的谓词
  - IN
  - 比较运算符
    - 内层查询返回单值时，才可以用比价运算符
  - ANY 谓词
    - 与比较运算符配合使用
    - 表示集合中**存在**值满足该比较关系
  - ALL 谓词
    - 与比较运算符配合使用
    - 表示集合中**所有**的值满足该比较关系
  - EXISTS 谓词
    - 不返回数据返回一个逻辑值（TRUE / FALSE）
    - 若内层结果非空，则外层返回真
  - NOT EXISTS谓词
    - 与EXISTS相反
  - FROM 子句中的子查询
    - 子查询返回的结果用作查询目标关系
  - WITH 子句
    - 定义临时关系，用于嵌套查询
  - 标量子查询

#### 集合查询



