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

    p125

