# MySQL笔记

* MySQL 语句的规范
  + 关键字与函数名全部大写
  + 数据库名称、表名称、字段名称全部小写
  + SQL 语句必须以分号结尾

* 修改 MySQL 提示符

  + 连接客户端时通过参数指定

    `shell>mysql -uroot -proot --prompt 提示符`

  + 连接上客户端后，通过 prompt 命令修改

    `mysql>prompt 提示符`

  + MySQL 提示符

    | 参数 | 描述       |
    | ---- | ---------- |
    | \D   | 完整的日期 |
    | \d   | 当前数据库 |
    | \h   | 服务器名称 |
    | \u   | 当前用户   |

* MySQL 常用命令

  + 显示当前服务器版本：

    `SELECT VERSION();`

  + 显示当前日期时间：

    `SELECT NOW();`

  + 显示当前用户：

    `SELECT USER();`

* 查看当前服务器下的数据库列表

  `SHOW {DATABASES | SCHEMAS} [LIKE 'pattern' | WHERE expr]`

* 创建数据库

  `CREATE {DATABASE | SCHEMA} [IF NOT EXISTS] db_name`
  `[DEFAULT CHARACTER SET [=] charset_name`

* 修改数据库

  `ALTER {DATABASE | SCHEMA} [db_name] [DEFAULT] CHARACTER SET [=] charset_name`

* 删除数据库

  `DROP {DATABASE | SCHEMA} [IF EXISTS] db_name`

  ### 数据类型

  * 数据类型是指列、存储过程参数、表达式和局部变量的数据特征，它决定了数据的存储格式，代表了不同的信息类型。

  * 整型

    `TINYINT、SMALLINT、MEDIUMINT、INT、BIGINT`

  * 浮点型

    `FLOAT[(M, D)]、DOUBLE[(M, D)]`

    > M 是数字总位数，D 是小数点后面的位数。如果 M 和 D 被省略，根据硬件允许的限制来保存值。单精度浮点数精确到大约 7 位小数位。

  * 日期类型

    `YEAR、TIME、DATE、DATATIME、TIMESTAMP`

  * 字符型

    | 列类型                        | 存储需求                                        |
    | ----------------------------- | ----------------------------------------------- |
    | CHAR(M)                       | M 个字节，0 <= M <= 255                         |
    | VARCHAR(M)                    | L + 1 个字节，其中 L <= M 且 0 <= M <= 65535    |
    | TINYTEXT                      | L + 1 个字节，其中 L < $2^8$                    |
    | TEXT                          | L + 2 个字节，其中 L < $2^16$                   |
    | MEDIUMTEXT                    | L + 3 个字节，其中 L < $2^24$                   |
    | LONGTEXT                      | L + 4 个字节，其中 L < $2^32$                   |
    | ENUM(‘value1’, ‘value2’, ...) | 1或 2 个字节，取决于枚举值的个数                |
    | SET(‘value1’, ‘value2’, ...)  | 1、2、3、4 或者 8 个字节，取决于 set 成员的数目 |

### 数据表

* 概述： 数据表（或称表）是数据库最重要的组成部分之一，是其他对象的基础。

* 打开数据库：`USE db_name`

* 创建数据表：

  ```sql
  CREATE TABLE [IF NOT EXISTS] table_name(
      column_name data_type,
      ...
  )
  ```

* 查看数据表列表：

  ```sql
  SHOW TABLES [FROM db_name]
  [LIKE 'patten' | WHERE expr]
  ```

* 查看数据表结构：

  ```sql
  SHOW COLUMNS FROM tbl_name
  ```

* 插入记录：

  ```sql
  INSERT [INTO] tbl_name [(col_name,...)] VALUES(val,...)
  ```

* 记录查找：

  ```sql
  SELECT expr,... FROM tbl_name
  ```

* 字段值：

  + NULL, 字段值可以为空
  + NOT NULL, 字段值禁止为空
  + AUTO_INCREMENT, 自动编号，且必须与主键组合使用，默认情况下，起始值为 1，每次的增量为 1
  + PRIMARY KEY: 主键约束，每张数据表只能存在一个主键，主键保证记录的唯一性，主键自动为 NOT NULL