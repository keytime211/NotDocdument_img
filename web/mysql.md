mysql常用命令



| 数据表                                                |                                                              |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| SHOW DATABASES;                                       | 查询数据表，列出                                             |
| SHOW TABALES;                                         | 查询数据表中的表单，列出                                     |
| CREATE DATABASE test_table;                           | 创建数据库                                                   |
| CREATE TABLE user(name varchar(10))                   | 创建表名name 可变字符串长度10                                |
|                                                       |                                                              |
| **增表**                                              | **alter    add modify change drop rename column**            |
| ALTER TABLE user ADD COLUMN id int;                   | 添加字段到user表字段名id数据类型为int                        |
| ALTER TABLE user MODIFY COLUMN name varchar(5);       | 修改字段数据类型这里把字段name数据类型修改成可变数据类型长度为5 |
| ALTER TABLE user CHANGE COLUMN id age int             | 修改字段名称把id修改成age同时也可以改变数据类型，这里需要指定类型否则会报错误 |
| ALTER TABLE user DROP COLUMN id;                      | 删除字段 id                                                  |
| ALTER TABLE user RENAME TO username;                  | 修改表名这里把user表名改成username                           |
| DESC username;                                        | 查看表数据结构                                               |
| DROP TABLE username;                                  | 删除username表                                               |
|                                                       |                                                              |
| **增加表单数据**                                      |                                                              |
| insert into user values(2,'lisi',18);                 | 在表中加入数据,没有定义字段就按创建顺序一一对应              |
| insert into user(id,name)values(1,'zhangsan')         | 在表中加入数据定义字段然后值一一对应                         |
| delete from user                                      | 删除全表数据                                                 |
| delete from user where id=2;                          | 删除id是2的这条数据,后面定义的id也可以name或者是age          |
| update user set name=''zhangsan';                     | 不按条件修改整个字段,就是字段为name所有的内容都修改成zhangsan |
| update user set name=''lisi' where id=1;              | 按条件修改字段,id是2的字段为name,的内容修改成lisi            |
| update user set name='kali',age=16 where id=2;        | 按条件修改多个字段,id=2,字段为name,age的内容修改成kali,16    |
|                                                       |                                                              |
| **基本查询**                                          |                                                              |
| select * from 表名;                                   | 查询表中所有字段                                             |
| select id,name from 表名;                             | 查询指定字段，这里查询id和name字段                           |
| select name as '姓名' from user;                      | 给表取别名as命令这里把name改为姓名                           |
| select distinct name from user;                       | 只是在查询的时候去除了重复项,实际数据还在表中存在            |
|                                                       |                                                              |
| **条件查询**                                          | **and(与)  or(或)   >  <  >=  <=  =  < > (between(区间) and)** |
| select * from user where id=3 and name='kali';        | 查询user表中id=3同时name='kali'的值列出来，两个条件要同时满足才可 |
| select * from user where id=2 or name='kali';         | 查询表中id=2和name='kali'的值列出来，这两个条件，只要有一个满足就会列出表中的值 |
| select * from user where age < 18;                    | 查询年龄小于18的数据                                         |
| select * from user where age > 18;                    | 查询年龄大于18的数据                                         |
| select * from user where age <> 18;                   | 查询年龄小于和大于18的数据，但不包括18                       |
| select * from user where age <= 18；                  | 查询年龄小于等于18的数据并列出表单                           |
| select * from user where age btween 17 and 20;        | 查询表中年龄是17到20之间的数据表单，并列出                   |
|                                                       |                                                              |
| **模糊查询**                                          | **ilke     %可以代替任意字符   _代替一个字符**               |
| select * from user where name like 'kal_';            | 注意这里 _ 只能代替一个参数，这里使用'ka_'是找不到'kali'的   |
| select * from user where name like 'k%'               | 查询%可以代替任意多个字符，所以这里只有一个'k'也可以找到'kali' |
|                                                       |                                                              |
| **分页查询**                                          | **查询某行到某行的数据 limit**                               |
| select * from user limit 2;                           | 查询开始到第二行的数据                                       |
| select * from user limit 2,5;                         | 查询第二行到第五行的数据                                     |
|                                                       |                                                              |
| **聚合查询**                                          | **max min avg(平均值)  count(统计表的纪录数量)**             |
| select max(age) from user;                            | 查询user表中年龄最大的值，并打印                             |
| select min(age) from user;                            | 查询表中年龄最小的并打印                                     |
| select avg(age) from user;                            | 计算并打印表中年龄的平均数                                   |
| select count(*) from user;                            | 统计表中的数据有几条                                         |
| select max(age),min(age),avg(age),count(*) from user; | 可以统一查询最大值最小值平均数和统计表中的数据               |
|                                                       |                                                              |
| **分组查询**                                          | **group by**                                                 |
| select age,count(*) from user group by age;           | 把所有age的值重新组合并统计age重复的数量，这里group by 后面的参数要和之前的定义的一样，这里是age后面就是age |
|                                                       |                                                              |
| **排序查询**                                          | **order by  asc升序A-Z    desc 降序 Z-A**                    |
| select * from user order by name asc;                 | 对user表name进行升序排列                                     |
| select * from user order by age desc;                 | 对user表中的age进行降序                                      |
|                                                       |                                                              |
| **常用查询数据库常量**                                |                                                              |
| select @@tmpdir；                                     | 查看临时目录                                                 |
| select @@datadir;                                     | 数据库存放位置                                               |
| select @@basedir;                                     | 数据库服务所在位置                                           |
| select @@version;                                     | 查看数据库版本                                               |
| select @@hostname;                                    | 查看当前的用户名                                             |
|                                                       |                                                              |
| **常用查询数据库函数**                                |                                                              |
| select char(97);                                      | 返回对应的ASCII码的字符,这里返回a                            |
| select ascii('a');                                    | 返回ASCII码对应的数字,这里返回97                             |
| select if(1=1,2,3);                                   | if逻辑1=1为true返回2,false返回3                              |
| select mid('admin',1,3);                              | 截取字符串这里截取1-3的字符串adm注意这里是从1开始而不是0     |
| select substr('admin',1,2);                           | 和mid是一样的                                                |
| select length('adminadmin');                          | 返回字符串长度，这里长度返回长度为10                         |
| select left('admin',4);                               | lef从左开始截取admin是被截取的字符串，4是截取的位数，这里是4，返回的就是admi |
| select right('admin',3);                              | right从右开始截取admin是被截取的字符串，3是截取的位数，这里是3，返回的就是nim |
| select user();                                        | 获取当前登陆用户名                                           |
| select version();                                     | 获取当前版本号                                               |
| select database();                                    | 获取当前数据库                                               |
| select sleep(3);                                      | 休眠，等三秒钟然后返回查询结果                               |





在表中插入数据的时候，如果字段没有定义全的话会显示null表示空