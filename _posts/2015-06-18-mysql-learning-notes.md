---
layout: post
title: "MySQL Learning Notes"
keywords: [mysql]
description: mysql
category: mysql
tags: [mysql, 数据库]
---
{% include JB/setup %}

## MYSQL

### 三. MySQL语句语法:

#### 一、数据定义语言: 第一: 创建
* 1 创建数据库/模式: CREATE DATABASE/SCHEME 语法

```
Syntax:
    create {database | schema} [IF NOT EXISTS] db_name
        [create_specification [, create_specification] ...];

    create_specification 选项:
        [DEFAULT] CHARACTER SET charset_name |
        [DEFAULT] COLLATE collation_name;

    # 栗子:
    1. create database blog;
    2. create database if not exist blog;
    3. create database blog;
        default character set utf8;
    4. create database if not exists blog
        default character set utf8;
    5. create schema blog
        default character set utf8;
```

* 2 创建索引: CREATE INDEX 语法

```
Syntax:
    CREATE [UNIQUE | FULLTEXTISPATIAL] INDEX index_name
        [USING index_type]
        ON tbl_name (index_col_name);
    
    index_col_name 选项:
        col_name [(length)] [ASC | DESC];

    # 栗子
    # show databses;
    # create database if not exist t;
    # use t;
    # show tables;
    # create table t (a int primary key auto_increment, b varchar(255));
    # desc table_name;
    create index t_index 
        on t (a desc, b);
```

* 3 创建表: CREATE TABLE 语法
        
``` Syntax
# Syntax
    CREATE [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
        [(create_defination, ...)]
        [table_option] [select_statement];
或
    CREATE [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
        [(] LIKE old_tbl_name [)];

create_defination:
    column_defination 
    | [CONSTRAINT [symbol]] PRIMARY KEY [index_type] (index_col_name, ...)
    | KEY [index_name] [index_type] (index_col_name, ...)
    | INDEX [index_name] [index_type] (index_col_name, ...)
    | [CONSTRAINT [symbol]] UNIQUE [index]
        [index_name] [index_type] (index_col_name, ...)
    | [FULLTEXTISPATIAL] [INDEX] [index_name] (index_col_name, ...)
    | [CONSTRAINT [symbol]] FOREIGN KEY
        [index_name] (index_col_name, ...) [reference_definition]
    | CHECK (expr)

column_defination:
    col_name type [NOT NULL | NULL] [DEFAULT default_value]
        [AUTO_INCREMENT] [UNIQUE [KEY] | [PRIMARY] KEY]
        [COMMET 'string'] [reference_defination]

type:
      TINYINT(length)       [UNSIGNED] [ZEROFILL]
    | SMALLINT[(length)]    [UNSIGNED] [ZEROFILL]
    | MEDIUMINT[(length)]   [UNSIGNED] [ZEROFILL]
    | INT[(length)]         [UNSIGNED] [ZEROFILL]
    | INTEGER[(length)]     [UNSIGNED] [ZEROFILL]
    | BIGINT[(length)]      [UNSIGNED] [ZEROFILL]
    | REAL[(length, decimals)]      [UNSIGNED] [ZEROFILL]
    | DOUBLE[(length, decimals)]    [UNSIGNED] [ZEROFILL]
    | FLOAT[(length, decimals)]     [UNSIGNED] [ZEROFILL]
    | DECIMAL(length, decimals)     [UNSIGNED] [ZEROFILL]
    | NUMERIC(length, decimals)     [UNSIGNED] [ZEROFILL]
    | DATE
    | TIME
    | TIMESTAMP
    | DATETIME
    | CHAR(length) [BINARY | ASCII | UNICODE]
    | VARCHAR(length) [BINARY]
    | TINYBLOB
    | BLOB
    | MEDIUMBLOB
    | LONGBLOB
    | TINYTEXT [BINARY]
    | TEXT [BINARY]
    | MEDIUMTEXT [BINARY]
    | LONGTEXT [BINARY]
    | ENUM(value1, vaule2, value3, ...)
    | SET(value1, value2, value3, ...)
    | spatial_type

index_of_col_name:
    col_name [(length)] [ASC | DESC]

reference_defination:
    REFERENCES tbl_name [(index_col_name)]
        [MATCH FULL | MATCH PARTIAL | MATCH SIMPLE]
        [ON DELETE reference_option]
        [ON UPDATE reference_option]

reference_option:
    RESTRICT | CASCADE | SET NULL | NO ACTION

table_options:
    table_option [table_option] ...

table_option:
      {ENGINE | TYPE} = engine_name
    | AUTO_INCREMENT = value
    | AVG_ROW_LENGTH = value
    | [DEFAULT] CHARACTER SET charset_name [COLLATE collation_name]
    | CHECKSUM = {0 | 1}
    | COMMENT = 'string'
    | CONNECTION = 'connect_string'
    | MAX_ROWS = value
    | MIN_ROWS = value
    | PACK_KEYS = {0 | 1 | DEFAULT}
    | PASSWORD = 'string'
    | DELAY_KEY_WRITE = {0 | 1}
    | ROW_FORMAT = {DEFAULT | DYNAMIC | FIXED | COMPRESSED | REDUNDANT | COMPACT}
    | UNION = (tbl_name[, tbl_name, ...])
    | INSERT_METHOD = {NO, FIRST, LAST}
    | DATE DIRECTORY = 'absolute path to directory'
    | INDEX DIRECTORY = 'absolute path to directory'

partition_options:
    PARTITION BY
          [LINEAR] HASH(expr)
        | [LINEAR] KEY(column_list)
        | RANGE(expr)
        | LIST(column_list)
    [PARTITIONS num]
    [ SUNPARTITION BY
          [LINEAR] HASH(expr)
        | [LINEAR] KEY(column_list)
      [SUBPARTITIONS(num)]
    ]
    [(partition_defination) [, partition_defination, ...]]

partition_defination:
    PARTITION partition_name
        [VALUES {
            LESS THAN (expr) | MAXVALUE | IN (value_list)
            }]
        [[STORAGE] ENGINE [=] engine_name]
        [COMMENT [=] 'comment_text']
        [DATA DIRECTORY [=] 'data_dir']
        [INDEX DIRECTORY [=] 'index_dir']
        [MAX_ROWS [=] max_number_of_rows]
        [MIN_ROWS [=] min_number_of_rows]
        [TABLESPACE [=] (tablespace_name)]
        [NODEGROUP [=] node_group_id]
        [(subpartition_defination) [, (subpartition_defination), ...]]

subpartition_defination:
    SUBPARTITION logical_name
        [[STORAGE] ENGINE [=] engine_name]
        [COMMENT [=] 'comment_text']
        [DATA DIRECTORY [=] 'data_dir']
        [INDEX DIRECTORY [=] 'index_dir']
        [MAX_ROWS [=] max_number_of_rows]
        [MIN_ROWS [=] min_number_of_rows]
        [TABLESPACE [=] (tablespace_name)]
        [NODEGROUP [=] node_group_id]

select_statement:
    [IGNORE | REPLACE] [AS] SELECT ... (some legal select statement)
```

``` CREATE TABLE 栗子
# 1. 最简单
create table Student
(
    sno int,
    sname varchar(10),
    cno int
);

# 2. INF: 原子性(主属性不为空NULL) + 主键(PRIMARY key) 
create table Student
(
    id int primary key auto_increment,
    sname varchar(10) not null,
    cname varchar(30) not null
);

# 3. 不存在才创建
create table if no exists Cost
(
    id int,
    money decimal(20, 2),
    date date,
    time timestamp,
    comment text,
    age integer(2),
    primary key (id)
);

# 4. 外键/外码: foreign key .... references ...
create table SC
(
    id int,
    sno int,
    primary key (id),
    foreign key (sno) references Student(sno)
);
desc SC;
show create table SC;
```