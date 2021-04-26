### 6种常见的约束

#### 1.default

- - 指定某列的默认值，插入数据时候，此列没有值，则用default指定的值来填充
  - create table t1(
    id int default 1,
    name varchar(20) default ‘老王’
    );

#### 2.not null

- 概念
  - 指定某列的值不为空，在插入数据的时候必须非空 ‘’ 不等于 null, 0不等于 null

#### 3.unique

- 概念
  - 指定列或者列组合不能重复，保证数据的唯一性
  - 不能出现重复的值，但是可以有多个null
  - 同一张表可以有多个唯一的约束

#### 4.auto_increment: 自增长约束

- 概述
  - 列的数值自动增长，列的类型只能是整数类型
  - 通常给主键添加自增长约束

#### 5.主键约束

- 概念
  - 当前行的数据不为空并且不能重复
  - 相当于：唯一约束+非空约束

#### 6.unsigned: 无符号约束

- 概念
  - 指定当前列的数值为非负数
  - age tinyint 1 -128～127 unsigned 0～255

#### 7.外键约束 foreign key

如果需要更好的性能，并且不需要完整性检查，可以选择使用MyISAM表类型，如果想要在MySQL中根据参照完整性来建立表并且希望在此基础上保持良好的性能，最好选择表结构为innoDB类型。

4、外键的使用条件

① 两个表必须是InnoDB表，MyISAM表暂时不支持外键

② 外键列必须建立了索引，MySQL 4.1.2以后的版本在建立外键时会自动创建索引，但如果在较早的版本则需要显式建立；

③ 外键关系的两个表的列必须是数据类型相似，也就是可以相互转换类型的列，比如int和tinyint可以，而int和char则不可以；

5、外键的好处：可以使得两张表关联，保证数据的一致性和实现一些级联操作。


#### alter的用法

1.改表名

ALTER TABLE admins RENAME TO users；

2.增加主键

alter table tabelname add new_field_id int(5) unsigned default 0 not null auto_increment ,add primary key (new_field_id);

可以做CHANGE所有事，除了重命名字段。

#### modify和change区别

change：

对列进行重命名时：
          < mysql> ALTER TABLE t1 CHANGE a b INTEGER。

    改列的类型而不是名称， CHANGE语法仍然要求旧的和新的列名称，即使旧的和新的列名称是一样的。
          <mysql> ALTER TABLE t1 CHANGE b b BIGINT NOT NULL.
也就是说改变字段的名字时候用change，否则基本用modify

modify：

Modify:
    使用MODIFY来改变列的类型，此时不需要重命名。
          <mysql> ALTER TABLE t1 MODIFY b BIGINT NOT NULL。

 

另：用alter修改一个列属性的时候，如果原来字段是允许null且有数据的字段为null时，更新列为not null会报错(必须先把所有的null属性都更新)


#### unsigned

unsigned 为“无符号”的意思 
  
unsigned 既为非负数，用此类型可以增加数据长度!

例如如果  tinyint最大是127，那  tinyint  unsigned  最大  就可以到   127 * 2

unsigned 属性只针对整型，而binary属性只用于char 和varchar。

 **unsigned**,zerofill  既为非负数，用此类型可以增加数据长度，  
  例如如果  int最大是65535，那  int  unsigned  zerofill  最大  
  就是  65535  *  2

|  tinyint  |                |
| :-------: | :------------: |
| smallint  |                |
| mediumint |                |
|    int    |                |
|  bigint   |                |
|   float   |  单精度浮点数  |
|  double   |  双精度浮点数  |
|  decimal  | 一个串的浮点数 |

