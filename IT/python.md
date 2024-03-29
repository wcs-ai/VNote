## 一、python：

### 1、环境安装：

**普通环境**：到官网下载 python 到本地，解压后路径添加到环境变量即可，如果没有装 pip，可到[pip 下载地址](https://bootstrap.pypa.io/get-pip.py)，下载到本地后，`python get-pip.py`就会开始安装。
**Anaconda 安装**：
windows 安装：进入[Anaconda 官网下载地址](https://www.anaconda.com/products/individual)下载；打开 Anaconda prompt 命令 窗口；自己 使用 pip 安装的第三方库会出现下载不全，子模块缺失等问题， 非常头疼，而安装 Anaconda 后在其中下载并使用它里面的软件进行编程则 不会出现问题。以 Anaconda2 开头命名的是对 python2 版本的支持,以 Anaconda3 开头的是对 python3 版本的支持。
进入 Anaconda 自带指令工具 Anaconda Prompt 的 base 环境安装各种第三方库后可以不用进入设置的虚拟环境中更不用使用 Anacaonda 中打开代码编辑工具就可以编程使用。
创建环境:使用 conda create -n name python=3.5 可以创建一个虚拟环境， name 名可随意起，后面是想使用的 python 的版本号。自己安装的 Anaconda 包目录下有一个 envs 文件夹(environments 的缩写)是放自己所创建的环境的。script 文件夹下是一些库附带的可直接运行的 cmd 命令程序，如 tensorboard。[python 官网下载地址](https://www.python.org/downloads/windows/)
<i class="red">进入环境</i>：windows 使用 activate name；linux 使用 source activate wcs.
<i class="red">安装库</i>：conda install scipy (安装的库在所有虚拟环境中可用)
<i class="red">卸载库</i>：conda remove scipy
<i class="red">更新包</i>：pip install --upgrade package_name conda update package_name
或 pip install 包名 --upgrade --ignore-installed 包名 #能忽略一些问题
<i class="orange">pip 安装包时提示权限不够：</i>安装时命令末尾添加--user
pip 和 conda 更新：若非要求，不要随便更新
pip install requests pip install requests --upgrade
conda install requests conda update requests
<i class="red">查看所有包</i>：conda list,[存在包库的地方:安装目录下的 Lib>site-packages,每个环境下的 Lib>site-packages 和安装目录下的 pkgs,如果想要做库的转译可以转到这三个目录试试]
注：打开 Anaconda Prompt 使用 conda install tensorflow 安装 tenforflow 框架，若
弹出提示有包与该框架冲突则将其卸载直到没有冲突的包为止，将删除的包做好记录
。在 Anaconda Prompt 也可以使用 pip 指令。各个环境安装的库不能共用
(当使用 conda 下载包时若出现中断或缓慢的问题可以尝试使用 pip 下载)
<i class="red">安装指定版本</i>：conda install cudatoolkit==8.0
<i class="red">在 Anaconda 中加入自己的库</i>：只要把自己的个人库放到相应的 python 环境中(site-packages 文件夹下)，就能向其它环境中的包一样导入使用。
Anaconda 下载 pytesseract 库：https://www.cnblogs.com/daacheng/p/9627136.html
<i class="red">安装后无法进入 base 环境问题</i>：不能安装在中文名文件下，需要加入环境变量。
<i class="red">linux 上的安装及使用注意：</i>到官网根据相应的 linux 系统下载或按命令指引下载包安装，安装过程中有指定安装路径位置，可以更改，回车则表示使用默认，若默认安装在/root 下则以后想要进入就需要切换为 root 模式进入，若未自动配置环境变量可以自行添加，位置是/root/anaconda3/bin<i class="violet">注意：似乎如果不安装在用户分区下面，在 vscode 中就检测不到 anaconda 环境，设置了也没用，所以还是尽量将其安装在用户分区下。</i>。
<i class="red">配置安装源和克隆环境：</i>conda create --name wcs --clone base #克隆已有的库，克隆 base 并命名为。若克隆环境的 pip 报错就将原克隆环境的 pip 包复制过来，bin/pip 文件的导入 main 的命令也改为和原环境的 bin/pip 一致。conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ # 配置库的下载源。[统一配置安装源](https://blog.csdn.net/hanguo1577717382/article/details/80245707)
[cannot import relative]relative 在 dateutil 包下，重新安装即可，但使用:pip install python-dateutil
<i class="red">pip 安装经常中断</i>：将外国的安装源改为国内的会有所改善：（-i 参数指定安装源）
Pip install rasa_core -i https://pypi.douban.com/simple
豆瓣：https://pypi.douban.com/simple 阿里：https://mirrors.aliyun.com/pypi/simple
清华： https://pypi.tuna.tsinghua.edu.cn/simple/ 中科大：http://pypi.mirrors.ustc.edu.cn/simple/

### 2、数据库：

**关系型数据库**：也叫 SQL 型数据库，表格的形式。可以用 SQL 语句方便的在一个表以及多个表之间做非常复杂的数据查询。对于安全性能很高的数据访问要求得以实现。`MY SQL/Oracle/PostgreSQL`等
**非关系型数据库**：NOSQL 型数据库。是基于键值对的，可以想象成表中的主键和值的对应关系，而且不需要经过 SQL 层的解析，所以性能非常高。`MongoDB/RethinkDB/DynomaDB`等。

> **Redis**:（Remote Dictionary Server )，即远程字典服务，是一个开源的使用 ANSI C 语言编写、支持网络、可基于内存亦可持久化的日志型、Key-Value 数据库，并提供多种语言的 API。

**图形数据库**：用图的结构构建的数据库，一般用于知识图片这类关系复杂的数据。Neo4j。
**SQL**：Structed Query Language 是用于访问和处理数据库的标准的计算机语言。而可以使用 sql 处理数据库的数据库有 MySQL、SQL Server、Access、Oracle、Sybase、DB2 等等。在进入到各数据库模式下后可以直接使用 sql 语句对数据库进行操作。
**分布式存储系统**：就是将用户需要存储的数据根据某种规则存储到不同的机器上，当用户想要获取指定数据时，再按照规则到存储数据的机器里获取。
当用户（即应用程序）想要访问数据 D，分布式操作引擎通过一些映射方式，比如 Hash、一致性 Hash、数据范围分类等，将用户引导至数据 D 所属的存储节点获取数据。

**mysql**：

#### a、安装及问题：

windows 上安装：安装包解压后进入文件夹创建一个`my-small.ini`文件。
【低版本】在文件最低部添加：basedir=该文件夹绝对路径 /n datadir=文件夹绝对路径/data。
【高版本】不要设置 datadir 参数，不然启动服务时报错，按照菜鸟教程走即可。
进入 bin 目录 cmd>>`mysqld --initialize --console `//初始化数据库。会输出初始账户，密码，请记住！！！

```sql
mysqld install MySQL//安装名为MySQL的服务。注意在管理员身份下运行命令。`c:>d:`#切换到d盘
mysqld --remove MySQL `//移除指定服务。
net start mysql //启动mysql服务 ，启动失败的话直接到服务列表手动启动即可。
mysql -h root -p //登录(初始密码为空)，
```

**使用前**：注意使用前必须修改用户密码，方法如下： :bulb:

```
D:\mysql\bin>mysql -u root -p    #目录下登入mysql
Enter password:****            #输入原密码进入
#进入到mysql模式，此时可使用sql等语句。每条语句后都要打分号再enter运行。
mysql>alter user root@localhost identified by 'xsww';将密码更改为xsww
```

<i class="label1">linux 上安装</i>[linux 上安装 mysql 学习地址。](https://blog.csdn.net/qq_40223688/article/details/90733495)

- mysql 的用密码设置是有规则要求的。[mysql 用户密码设置规则。](https://www.cnblogs.com/pythonywy/p/11815028.html)
- mysql 服务管理(linux)：

```
service mysqld status    //查看服务状态
service mysqld stop //关闭
service mysqld start //开启
service mysqld restart    //重启
```

**问题集**：

- 提示找不到 VCRUNTIME140_1.dll：安装微软常用库。
- mysqld isntall 服务时提示：Install/Remove of the Service Denied!#可进入<i class="red">管理员身份运行</i>。
- 其它软件连接 mysql 需要使用 mysql 驱动包，[mysql 驱动包下载地址。](https://mvnrepository.com/artifact/mysql/mysql-connector-java)。
- mysql 的 jdbc 驱动 6.0 版本以上需要设置 time zone，可以在连接 url 中设置：`jdbc:mysql://localhost:3306/test?serverTimezone=GMT%2B8`。
- 忘记 root 密码的方法：

```
mysqld --skip-grant-tables &    //进入bin目录下执行
mysql -u root                   // 然后能跳过密码进入mysql模式
mysql> update user set password=password('123') where user='root' and host='localhost';    //修改了新的密码，再退出登录即可
```

- [连接 mysql 时提示：Authentication method 'caching_sha2_password' is not supported 解决方法](https://blog.csdn.net/u011583336/article/details/80999043)。

#### b、可视化：

**mysql 可视化管理工具**：navicat for MySQL 破解：https://blog.csdn.net/wypersist/article/details/79834490
<i class="label1">mysql 数据表与 csv 文件互导</i>简单的操作可使用 navicate 的导入直接将一个 csv 文件转为一个新表。
使用命令导入则需要先建立一个新表(数据类型使用 varchar)，然后将文件导入该表。导入的文件放到安装时 my.ini 配置文件中 datadir 或 basedir 指定的文件夹中去，不然会被认为不是安全的文件。
**SQLyog**：

- 连接数据库时错误 password not be loaded：进入 mysql>，输入：`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';`再连接即可
  [null 值相关控制。](https://blog.csdn.net/duckyamd/article/details/53143639)[mysql 数据表与 csv 文件互导。](https://www.cnblogs.com/luruiyuan/p/5713273.html)

#### c、连接 mysql 

```py
from mysql import connector #pip install mysql-connector    和pymysql库一样的使用方法。
#连接mysql,主机名(ip),..database指定连接到的数据库，没有的话则只是连接mysql
wcs=connector.connect(host='localhost',user='root',passwd='',database='mysql')
ac=wcs.cursor()#创建一个光标用于操作mysql
#execute()执行sql语句来操作mysql，SHOW DATABASES展示数据库
ac.execute("SHOW DATABASES")#SHOW TABLES 显示当期库下的所有表格
for x in ac:print(x)#查看所有数据库或当期数据库下的所有表格；配合上面的语句

# 若上面没有指定连到哪个数据库的话，需要先ac.execute("use mysql")

# 在查询时
val = ac.execute("SELECT * FROM user")    #选取所有列
print(val)#列的数量，直接使用sql语句时还会显示各行的键类型、等其它属性。
```

**增、删、查、改**：
//插入数据,（增）。单条插入,使用占位符%时 execute()内需要填两个值

```py
sql = "INSERT INFO sites (name,url) VALUES (%s,%s)"
ac.execute(sql,('wcs','http:'))#批量插入操作，第二值传入一元组,改成executemany()即可
ac.executemany(sql,[('google','url'),('github','url'),...])
wcs.commit()#涉及到更改数据库的操作需要使用commit()提交。

#查找数据,(查)。查找表sites中的所有数据

ac.execute("SELECT * FROM sites")#"SELECT name FROM sites"只查找name字段数据，选多个列时用逗号隔开。
#"SELECT * From sites ORDER BY name DESC"按name字段排序，默认升序，DESC为降
#"SELECT * FROM sites WHERE name = 'google'" 按条件查询
#定义占位符，避免sql注入攻击
sql1 = "SELECT * FROM sites WHERE name = %s"
ac.execute(sql1,("wcs",))#第二个参数必须是一个元组或列表
res=ac.fetchall()#获取到结果的一个迭代对象，需要使用for循环来获取

#删除表数据"DELETE FROM sites WHERE name = %s"不用WHERE的话会删除说所有数据
#更新数据，修改数据,更新name为wcs的数据为xsww

sql2 = "UPDATA sites SET name = 'xsww' WHERE name = %s"
ac.execute(sql2,('wcs',))
wcs.commit()

```

#### d、sql 语句：

<i class="label1">SQL</i>注意，虽然是 sql 语句，但在不同的数据库中可能用法略有不同。这里是 mysql 中可用的语句形式。
进入到 mysql 模式以后如下： 以下语句大小写均支持。
<i class="label2">查看部分</i>

```sql
show databases;    //显示所有已有的数据库
use mysql;    //选择其中一个数据库
SHOW TABLES;    //显示该库下的所有表
//查看表db的所有列，或用DESCRIB from db;效果一样。显示的Field项就是它的所有列，后面还有type等各列的属性描述。
SHOW COLUMNS from db;
//    其它SHOW命令。
SHOW STATUS：显示广泛的服务器状态信息
SHOW CREATE DATABASE 和 SHOW CREATE TABLE：显示创建特定数据库或表
SHOW GRANTS：显示授权用户（所有用户或特定用户）的安全权限
SHOW ERRORS 和 SHOW WARNINGS：显示服务器错误或警告消息
HELP SHOW：显示允许的SHOW语句
SHOW create table games;    //查看表games的所以有列属性，及使用的字符集编码
show create database wcs; //查看数据库详情。
```

<i class="label2">增、删、查、改</i>

```sql
/***************建库建表*/
create database wcs character set utf8;    #创建一个名为wcs的库。
#在当前库下建一个名为blogs的表。括号中的是表的字段，列名、数据类型。
create table blogs(id char(20) primary key,user_id char(20),name char(20) COMMENT '姓名',)character set utf8;
/*删除数据表 "DROP TABLE IF EXISTS sites"   IF EXISTS为判断*/

/***************修改操作，字段操作*/
alter table 表名 modify column 字段名 类型；
ALTER TABLE 表名 ADD COLUMN 字段名 numeric(18,0);    #添加
ALTER TABLE games DROP COLUMN id;    //删除某一个列。

/**********删除操作*/
DELETE FROM games WHERE id=15;    //删除id为15的那行。
DELETE FROM games WHERE year is null;    //剔除空值。
DELETE FROM gamse;    //删除所有的行。
DROP TABLE games;    //删除整个表。

/*************插入操作*/
INSERT INTO table VALUES (v1,v2,v3);    #直接插入值
INSERT INTO table (id,name,url) VALUES (1,'wcs','http://');    #指定键值的插入。
INSERT INTO table2 SELECT * FROM table1;    #从表1中选择一些字段插入到表2中。
/*    注意：插入就会新增行，即使你要插入的那列值之前的是为空，也会从表尾插入。*/
/*    DELAYED插入数据会做延迟操作，如果在插入期间有查询操作的话，会暂缓这些插入。*/
INSERT DELAYED INTO games (name) VALUES ('qq');


/*******更新操作,UPDATE操作一般比较费时间。*/
UPDATE games SET ys=10,avg_al=22.45 WHERE id=10;    //查找指定行，更新指定列值。


/*查询语句**************SELECT,WHERE是接一个字句。    可选择从多个表中查询*/
SELECT shop_id,item_id FROM test1,test2 LIMIT 2;    #LIMIT限制返回的条数。对应sql的TOP作用。    有子句时写在子句后。
SELECT DISTINCT country FROM Websites;    #DISTINCT选取country列中所有的项(去除了重复部分)。
/*like可指定用后面的匹配项去匹配指定列中满足条件的数据。第一个item_id是要显示的列，第二个item_id是要用于匹配的。*/
SELECT item_id from test WHERE item_id LIKE '24%';    /*#LIKE可用来匹配符合规则的数据。24%表示以24开头的。*/
SELECT * FROM Websites WHERE name REGEXP '^[GFs]';    /*#REGEXP后面使用正则表达式。*/
SELECT * FROM test WHERE name IN ('wcs','xsww');    /*#精确的查找，IN指定name字段中，在指定值内的数据。*/
SELECT * FROM test WHERE item_id BETWEEN 1 AND 20;    /*#BETWEEN指定一个范围。包括字符串范围。'a' AND 'z'*/
SELECT * FROM test WHERE item_id NOT BETWEEN 1 AND 20;    /*#NOT取反向，还能加在IN前面。*/
/*    多条件查询时的写法。用and链接，条件太多时，可能要拼接。*/
SELECT shop_id,item_id FROM test WHERE shop_id IN (59,24) and mount NOT BETWEEN 2 AND 5 LIMIT 10;
/*    用AS来为前一个表名或列名重新命名。*/
SELECT w.name, w.url, a.count, a.date FROM Websites AS w, access_log AS a WHERE a.site_id=w.id and w.name="菜鸟教程";
/* *****检测空值，库中显示为None*/
SELECT id,year FROM games WHERE year is null;    //使用year=null不能检测出来。*/


/* 通配符，通常与LIKE和REGEXP 一起使用。*/
/*%    #代替0个或多个字符，aa%表示以aa开头，%aa%则可匹配字符中任意位置的aa字符。*/
/*-    #代替1个字符。
[charlist]    #匹配到中阔号中任一字符。
[^abc]    #非括号中的字符。

/*    多张表一起查询。不过SELECT后要选择是哪个表的列名，不然报错。*/
SELECT test.Coupon_id FROM test,offline WHERE test.Coupon_id=offline.Coupon_id LIMIT 10;

/*    聚合函数：*/
SELECT round(avg(sales),3) as rd FROM games;
count() 求值的个数、sum() 求值的和、avg() 平均数、max() 最大值、min() 最小值
year()    getdate()#返回系统当前时间    month() day()#    year(GETDATE())#放到其它对应的函数中获取当前年份、月份等。

/*    GROUP BY的使用：表示通过某个字段进行分组，一般与聚合函数使用。当然可以和WHERE一起使用，并不冲突。*/
SELECT sum(mount) as '销量' FROM test GROUP BY shop_id;    #表示通过shop_id进行分组，然后计算各店铺的总销量。
SELECT sum(mount) FROM test WHERE area="云南" GROUP BY shop_id;    #表示选择云南的店。
/******多条件的group by。name和str_time一样时才分为一组*/
SELECT name,sum(money) FROM users GROUP BY name,str_time;

/*    having子句的使用：与WHERE类似，都是用于条件划分的。不过having是放在group by语句后用于筛选组的。*/
SELECT item_id,AVG(mount) FROM test GROUP BY shop_id having AVG(mount)>20;    #选出平均销量大于20的商店的信息。
/* 剔除空值*/
SELECT User_id FROM test WHERE
/*    查询最大值，这项稍有点特殊：*/
SELECT MAX(mount) FROM test WHERE shop_id=59;    MAX放在查询项而不是条件项。

/*    ORDER BY的使用*/
SELECT shop_id FROM test ORDER BY mount asc;    #asc是升序，desc是降序。
SELECT shop_id FROM test GROUP BY shop_id ORDER BY sum(mount);#    mount中不含有sum(mount)值。

/*   select嵌套使用：*/
SELECT shop_id FROM test WHERE mount=(select max(mount) from test);    #第二个select查询的结果作为第一个select句的条件值使用。

/*    EXISTS的使用：只返回布尔值，前面可加not配合使用。后面语句返回为True时才会执行前面的语句，否则返回empty set.*/
SELECT shop_id FROM test WHERE EXISTS(select shop_id from test where shop_id==60);

/* JOIN,联表查询，INNER JOIN 指定联合哪个表，ON指定用哪个列来联合，一般用同列名。*/
/* INNER JOIN返回的查询结果是两表最大相同公共长度结果集。而LEFT JOIN 和 RIGHT JOIN 则分别是返回以左或右表的最大结果集。*/
SELECT a FROM test INNER JOIN train ON test.b=train.b
/*指定多条件的链接*/
SELECT * FROM t1 INNER JOIN t2 ON (t1.name,t2.money) = (t2.name,t2.money + 1);


/*    UNION语句使用,联合多个查询语句。*/
SELECT name FROM tab1 UNION SELECT name FROM tab2;       /*如果两个表对应列中查出的值有重复会被合并，得到一个列表结果*/
SELECT name FROM tab1 UNION ALL SELECT name FROM tab2;   /*UNION ALL则不会合并重复的值。*/
```

[两个表联合。](https://www.jb51.net/article/154006.htm)
<i class="label2">特殊部分</i>

```sql
/*OVER()函数需要配合row_number(),rank(),dense_rank()等一起使用。*/
/*partion by type表示按照type字段来分组。order by sales表示按sales字段来排序*/
/*row_number()会对select结果的每条数据进行编号(每一组都从1开始编号)，结果类似:分好组，拍好序，编好号，但是返回一个一维的*/
SELECT id,type ROW_NUMBER() OVER(partition by type order by sales) as ord FROM games;
/*类似运用为查找各部分薪水前3的人*/
with tba as (SELECT Name,ROW_NUMBER() over(partition by did order by Salary) as rnk,Salary,did FROM Employee) SELECT tba.Name,Salary,dpt.Name as Department,Salary FROM tba LEFT JOIN dpt ON tba.did=dpt.id  WHERE tba.rnk<3;

/******with as的使用。定义一个sql片段，可被引用，类似于sql子句功能*/
/*用ntb代表括号内的查询结果，后一个select语句的FROM需要指定ntb才能使用ntb中的值*/
with ntb as (SELET id,name FROM users) SELECT id,name FROM ntb WHERE ntb.name LIKE 'w%';
/**数据类型转换
第一个参数为值，第二个为数据类型。char(19)表示从头开始取19个为字符串。
其它类型：DATE>日期。TIME(时间)、DATETIME、DECIMAL、SIGNED(整数)、 UNSIGNED(无符号整数)。
*/
SELECT CONVERT('2020-09-05 16:32:04',char(19));
SELECT CAST('3.35' AS signed); /*与convert一个作用*/

/****         找出连续3天消费金额超过100的用户。*/

/*将消费时间转换为字符串，后面用于分组*/
/*gp1,gp2,gp3都一样，计算用户单天的总消费，而且按（name,sale_time）分组，再将时间字符串转为时间格式，便于后面计算*/
/*按(name,time)=(name,time+1)的形式连接3个表，这样得到的一条数据就是用户连续3天消费的记录。*/
/*再条件筛选3天的金额超过一定值。其它类似情况也可以借鉴此写法。*/
with nt as (SELECT id,name,money,CONVERT(sale_time,char(10)) as t FROM user_cord),
gp1 as (SELECT name,CONVERT(t,DATE) as t1,sum(money) as ms FROM nt WHERE nt.name=nt.name GROUP BY nt.t,nt.name),
gp2 as (SELECT name,CONVERT(t,DATE) as t1,sum(money) as ms FROM nt WHERE nt.name=nt.name GROUP BY nt.t,nt.name),
gp3 as (SELECT name,CONVERT(t,DATE) as t1,sum(money) as ms FROM nt WHERE nt.name=nt.name GROUP BY nt.t,nt.name)
SELECT * FROM gp1 LEFT JOIN gp2 ON ((gp1.t1 + interval 1 day),gp1.name) = (gp2.t1,gp2.name)
LEFT JOIN gp3 ON (gp2.name,(gp2.t1 + INTERVAL 1 day)) = (gp3.name,gp3.t1)
WHERE gp1.name=gp2.name AND gp2.name=gp3.name AND (gp1.ms + gp2.ms + gp3.ms) > 100;

/*replace的使用，要进行多次替换操作时可使用这两种模式*/
with a as (SELECT name,REPLACE(obj,'数学',0) as zr FROM students) SELECT name,replace(zr,'语文',1) as sci FROM a;
SELECT name,REPLACE(REPLACE(obj,'数学',0),'语文',1) as sci FROM students;
/*更新操作时进行替换*/
update test_tb set address=replace(address,'东','西') where id=2：

/*排序函数：rank(若有相同值，排名一样，但接下来排名序号不连续)。
dense_rank(出现相同值情况也会有连续的排名序号)的使用*/
SELECT rank() over(order by score) as sf FROM students;
SELECT dense_rank() over(order by score) as sf FROM students;
```

#### e、字段属性及建表原则：

|   数据类型    |              含义              |   数据类型   |         含义         |  数据类型  |            含义             |
| :-----------: | :----------------------------: | :----------: | :------------------: | :--------: | :-------------------------: |
|     date      | 3 字节，日期，格式：2014-09-18 |   tinyint    |     （-128~127）     |  char(n)   |  固定长度，最多 255 个字符  |
|     time      |   3 字节，时间格式：08:42:30   |   smallint   |   （-32768~32767）   | varchar(n) | 可变长度，最多 65535 个字符 |
|   datetime    |        8 字节，日期时间        |  mediumint   | （-8388608~8388607） |  tinytext  |  可变长度，最多 255 个字符  |
|   timestamp   | 4 字节，自动存储记录修改的时间 |     int      |                      |    text    |                             |
|     year      |              年份              |    bigint    |                      | mediumtext |                             |
|     float     |      4 字节，单精度浮点型      | double(m, d) | 8 字节，双精度浮点型 |  longtext  |                             |
| decimal(m, d) |      存储为字符串的浮点数      |              |                      |            |                             |

**数据类型属性**：

- auto_increment：新插入的行赋一个唯一的整数标识符。每个表只允许一个。
- binary：只用于 char 和 varchar 值。当为列指定了该属性时，将以区分大小写的方式排序。与之相反，忽略 binary 属性时，将使用不区分大小写的方式排序。
- default：确保在没有任何值可用的情况下，赋予某个常量值。如 default NULL。
- null，not null：允许和不允许空值。
- primary key：用于确保指定行的唯一性。指定为主键的列中，值不能重复，也不能为空。常与 auto_increment 使用。
- unique：属性的列将确保所有值都有不同的值，只是 null 值可以重复。
- zerofill：可用于任何数值类型，用 0 填充所有剩余字段空间。

**建表原则**：

1. 表示是否...概念的字段必须用：is\_...格式命名，数据类型为 tinyint，属性为 unsigned。
2. 表名、字段名必须使用小写字母或数字，禁止出现数字开头，禁止两个下划线中间只出现数字。
3. 表名，字段名等禁用保留字，如 desc、range、match、delayed 等。
4. 小数类型为 decimal，禁止使用 float 和 double。[//]: #float 和 double 的存储的时候，存在精度损失的问题，很可能在值的比较时，得到不正确的结果。如果存储的数据范围超过 decimal 的范围，建议将数据拆成整数和小数分开存储。
5. 如果存储的字符串的字符长度几乎相等，使用 char 定长字符串类型。
6. varchar 是可变长字符串，不预先分配存储空间，长度不要超过 5000，如果存储长度大于此值，定义字段类型为 text，独立出来一张表，用主键来对应，避免影响其它字段索引效率。
7. 建表时，id，创建时间、更新时间都要带上，操作如下：

```sql
CREATE TABLE users(id smallint primary key auto_increment,create_time timestamp DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',update_time timestamp NULL DEFAULT NULL ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间');
```

8.库名与应用名一致，表明为业务名加作用。 9.单表行数 超过 500 万行或者表单容量超过 2GB，才推荐进行分库分表。 10.合适的选择整型、字符型，既节约空间又节约时间。
[建表原则学习地址。](https://www.jianshu.com/p/b7aaa973dc1d?from=timeline&isappinstalled=0)
可设置的数据类型：[mysql 中可设置的数据类型](https://www.cnblogs.com/cqlb/p/9856841.html)。[建表时设置字段属性。](https://www.jianshu.com/p/c6ca399b88ae)

#### f、日期相关计算：

```sql
 /*返回指定日期上添加天数后的日期，interval指定值和类型，还有year、day、hour、minu、second*/
SELECT DATE_ADD('2020-03-20',interval 2 month);
SELECT DATE_SUB('2020-03-20',interval 2 day);    /*和上面相反*/
SELECT '2020-07-20 13:55:02' + INTERVAL 2 MONTH;    /*或者直接这样计算。*/
/* CURDATE()#返回当前日期、CURTIME()#返回当前时间、NOW()#当前日期和时间*/
select SEC_TO_TIME(2378);//转为》时：分：秒表示。
SELECT TIME_TO_SEC('22:23:00');//转为总的秒数。
select WEEKDAY('1997-10-04 22:23:00');/*返回日期对于的星期，0为星期一。**/
/******查询时直接比较时间前后.    大于是指在这时间之后，小于则是在此之前*/
SELECT id FROM create_time > "2020-06-23 18:05:22";
/*转换时间格式,注意小写m表示月份，M表示分钟，这样可以将日期中的时间去掉*/
SELECT DATE_FORMAT(create_time,"%Y-%m-%d") as t FROM users;
```

#### g、备份与恢复：

备份会将表的创建命令，数据转为一条条插入命令存储为一个文件，恢复时再按照格式运行其中的命令。[参考学习地址。](https://blog.csdn.net/weixin_34345560/article/details/92419746)

```bash
/*非mysql模式下使用，wcs为指定的库，tools为其下面的表，多个表时空格隔开即可，最后指定路径文件*/
/*不指定表时，默认备份所有表*/
mysqldump -u root -p wcs tools > /home/wcs/back.sql
// 备份所有库
mysqldump -u username -p --all-databases > BackupName.sql
```

**其它数据库及使用选择**：

- sccess，foxbass：负载量 100 人以内，对安全性要求不高时可选择。
- mysql、sql server、informix：日访问量 5000 ～ 15000，如商务网站。
- sybass、oracle、db2：负载量大，安全性高，成本也较贵。

**数据迁移**：常会遇到把外面的离线数据倒入到当前使用的库中、把当前使用中的库迁移到一个新的库或服务器上、数据太多时分库分表、更新数据库版本，更换数据库引擎等，这些操作在停机情况下进行操作还算简便，但一般要求固定时间内完成，压力较大。**在线数据迁移**：可以不停机的情况下进行迁移，迁移完成后切换成新的库使用即可，对新库和旧库进行一个双写操作，即涉及到插入、更新、删除的操作在两个库同时进行，然后按顺序从旧库中将数据复制到新库中(迁移完后再做一遍数据校验，以旧库数据为准)。
[一篇较详细的数据迁移文章。](https://www.cnblogs.com/skying555/p/8479471.html)

#### h、回滚与日志：

**回滚**：用于操作失误后便于撤回。一种方法是使用备份的数据，结合查询日志来恢复数据，非常麻烦。另一种这是安装 binlog2sql，回滚起来极为简便。
centos 上安装 binlog2sql：`git clone https://github.com/danfengcao/binlog2sql.git && cd binlog2sql`#然后进入到 binlog2sql 文件目录中，`pip install -r requirements.txt`#安装文件中列出来的包。再进入 binlog2sql，将里面的 binlog2sql_util.py 文件移到 python 环境中，`Anaconda/bin`和 scikit-packages 中。
mysql 配置文件中添加配置：

- linux 上的 mysql 配置文件一般在/etc/my.cnf，win 则在 my.ini 中。
- 若是 linux 则添加：`log-bin=mysql-bin`和`server-id=1`两项。
- 重启服务：service mysqld restar
- 进入 mysql 模式：然后`show variables like ‘log_%’;`#查看 bin_log 状态。`show master logs;`#查看日志记录，一般非查询操作都会生成一条记录，似乎退出重启服务后才能看到最新的。
- 预览生成的回滚 sql：

```bash
#在刚才下载的binlog2sql中执行，binlog2sql.py是对应的文件。-u后的是用户名，-p后的是密码，注意修改。
python binlog2sql.py -h127.0.0.1 -P3306 -uroot -p'xsww' -dtest -t f --start-file='mysql-bin.000002' --start-pos=4 --end-pos=314 -B
# 回滚。
#mysql-bin.0000002是要恢复的日志记录。
python binlog2sql.py -h127.0.0.1 -P3306 -uadmin -p'admin' -dtest -t f --start-file='mysql-bin.000002' --start-pos=4 --end-pos=314 -B | mysql -h127.0.0.1 -P3306 -uadmin -p'admin'
```

**日志查看**：[日志查询学习参考地址。](https://www.cnblogs.com/mungerz/p/10442791.html)
日志类型：进入 mysql 模式可查询日志。

- 错误日志：错误日志功能是默认开启的，而且无法被关闭。`show global variables like 'log_error%';`#还有 log_warning。返回具体文件位置，可 vim 查看内容。
- 查询日志：默认情况，查询日志是关闭的。因为查询日志会记录用户所有的操作，导致不必要的磁盘 IO。
- 慢日志：慢查询日志是用来记录执行时间超过指定时间的查询语句。通过慢查询日志，可以查找出哪些查询语句的执行效率很低。`show global variables like 'long%';`
- 事物日志：事务日志（InnoDB 特有的日志）可以帮助提高事务的效率。
- 二进制日志：二进制日志也叫作变更日志，主要用于记录修改数据或有可能引起数据改变的 mysql 语句，并且记录了语句发生时间、执行时长、操作的数据等等。

```sql
show global variables like "%log_bin%";
#查看二进制日志内容。
show binlog events in 'mysql-bin.000002';
```

### 3、面向对象：

**类的内置函数**：双下划线开头，双下划线结尾，一部分是构建类时就会运行，这些内置函数用于管理类，是设计模式常用的手段。介绍如下：[类中各内置函数作用。](https://www.cnblogs.com/jinqi520/p/9814718.html)

- `__new__()`#在**init**()之前运行。若要接受参数，那么两者的参数量必须保持一致。
- `__init__(self)`#任意一个方时都会执行一次类中的**init**函数,若要调用类中的方法得先将该类赋值给另一个变量，然后由该变量调用类中的函数。可设置类接收的参数：

```py
class animal():#类中不一定要写这个初始化函数，但每个函数都要传入self
    def __init__(self):
        self.name='animal'
    def a(self):
        print(“hello”)
b = animal()
b.a()

```

[继承，多继承]不推荐使用多继承，多数编程语言中也不支持多继承，这在逻辑上会比较复杂

```py
class animal(object):
    def eat(self,data):
        return data*2

class plant(object):
    def drink(self,data):
        return data*3

//如果3个类中有重复的方法则会报错
class dog(animal,plant):#继承两个父类，若第一个父类没构造函数会从左
    #向右查找，把第一个有构造函数的类设为self域。
    def __init__(self,name):
        animal.__init__(self)#先运行父类的初始化，这样父类中的实例

    #才能在子类中直接使用self调用
        self.name = name#推荐先初始化父类的初始化函数。
        self.info = animal.eat(self,5)#这样调用父类中的函数
   @classmethod#它对应的函数不需要实例化，不需要self参数，但是第一个参数
    #需要是表示自身类的cls参数，可以用来调用类的方法，类的属性，
   def ability(cls):
       print(cls.num)
       return data

dog2 = dog('dog2')
v = dog2.drink(12)

#super()的使用
class pig(animal):
    def __new__(cls):
    #super()函数用于调用第一个参数的父级的一个函数,然后调用父类的方法。python3可直接写为：super().eat()
    #如果没有父类的话则调用本类。单继承时可不用。
        super(pig,cls).eat(cls)
```

### 4、爬虫：

python2 方法：

```py
url = “http://www.huaban.com”
Req = urllib2.Request(url，data,header)#3个参数
Res = urllib2.urlopen(Req,timeout=10)#2个参数
print Res.read()
```

python3 方法：
<i class="label1">简单爬取</i>

```py
import requests
url = “http://www.huaban.com”
s = request.get(url=url)
print(s.text)

from bs4 import BeautifulSoup
//BeautifulSoup是一个html解析器
bf = BeautifulSoup(html)//html是上面获取到的网页内容
//find_all()方法按条件查找：标签名、类名、id名,返回一个列表
content = bf.find_all('div',class_='a',id='k')
print(content[0].text)//返回的是带着标签的列表，用text获取标签内文本内容。

```

若未获得内容则有可能是网页设置了需要头部请求,打开要扒的网页打开 f12 下的
Network 项查看 Response header 中的内容,注意其中的 User-Agent,Content-Type,Referer 项，将其内容写到头部字典中一并发送 出去.
<i class="label1">SSL 验证</i>ssl 是 http 上加的一层协议，用上面的方法直接爬取可能会报 SSLError，这是需要做 ssl 验证，如下方法解决：

s = request.get(url=url,verify=False) //verify 设为 false 来绕过验证。

<i class="label1">抓包</i>在爬取一些由 js 动态加载(ajax)出来的数据的网页时，获取到的是未加载出数据的页面(一般是.html 页面)，此时就需要探查这个网页做了哪些请求，请求的接口等信息，浏览器控制台 network 项中可以查看请求记录，不过使用专门的抓包工具会更简便好用。
这里使用抓包工具：Fiddler。[Fiddler 下载地址(所有系统都支持)。](http://www.telerik.com/fiddler)(进入 Fiddler 后，可以打开浏览器进入一个网站，然后 Fiddler 就能监听到这台计算机作出的网络请求，将信息列出来)
<i class="label1">头部请求设置</i>js 向后台发送请求时，可以设置头部信息来控制要传的数据类型，规定验证信息等东西来做一个反爬虫的东西(后台配合)。以下是几个重要的头部：
User-Agent：这里面存放浏览器的信息。可以看到上图的参数值，它表示我是通过 Windows 的 Chrome 浏览器，访问的这个服务器。如果我们不设置这个参数，用 Python 程序直接发送 GET 请求，服务器接受到的 User-Agent 信息就会是一个包含 python 字样的 User-Agent。如果后台设计者验证这个 User-Agent 参数是否合法，不让带 Python 字样的 User-Agent 访问，这样就起到了反爬虫的作用。这是一个最简单的，最常用的反爬虫手段。
Referer：这个参数也可以用于反爬虫，它表示这个请求是从哪发出的。可以看到我们通过浏览器访问网站，这个请求是从https://unsplash.com/，这个地址发出的。如果后台设计者，验证这个参数，对于不是从这个地址跳转过来的请求一律禁止访问，这样就也起到了反爬虫的作用。
authorization：这个参数是基于 AAA 模型中的身份验证信息允许访问一种资源的行为。在我们用浏览器访问的时候，服务器会为访问者分配这个用户 ID。如果后台设计者，验证这个参数，对于没有用户 ID 的请求一律禁止访问，这样就又起到了反爬虫的作用。

headers = {'authorization':'your Client-ID'} # 这里的 your client-ID 是抓包中获得的，后面再补充。
req = requests.get(url=target, headers=headers, verify=False)

爬取 js 动态加载数据的网页的方法：https://www.znian.cn/932.html
[w3c 的 python3 爬虫教程地址。](https://www.w3cschool.cn/python3/python3-enbl2pw9.html)

**监听网络请求**：[参考学习地址](https://www.cnblogs.com/xuanhun/p/5625186.html)

### 5、Django 和 flask 的使用:

<i class="label1">django 安装</i>下载地址https://www.djangoproject.com/download/，使用git下载到本地后使用python来安装(也可以使用pip或conda安装，下载的和地址下载中的django文件夹一样)，进入到下载好的django目录下使用命令：python setup.py install //如果想安装到 anaconda 环境中使用其 python 对应系统变量即可。安装后在 python 环境中的 script 文件夹下会有 dnango-admin.exe 文件可以直接在 cmd 中使用,cmd 中输入 django-admin 能运行则成功。(若无法全局使用 django-admin 的话直接进入 scripts 文件夹下去运行即可。)
**配置 HTTPS**：[配置教程。](https://blog.csdn.net/qq_33183456/article/details/102967838)
**开始一个项目**：django-admin startproject HelloWorld //创建一个 HelloWorld 目录,
里面有一些初始化文件，再使用命令：python manage.py runserver 0.0.0.0:8000,然后在浏览器输入 127.0.0.1:8000 即可看到初始化页面。在 urls.py 文件配置如下：

```py
from django.conf.urls import url
#2.0以后的版本的path在django.urls下,1.0所属版本在conf.urls下
from django.urls import path
#from django.conf.urls import path
from . import view#这样写直接运行view文件可能会报错,不过cmd运行不会
#导入非环境中的包必须这样，否则会报错;导入anaconda中的包没问题
#urlpatterns中配置接口路径对应的指定页面中的函数，可以全部改成url配置
urlpatterns = [url(r'^$',view.hello),path('index/',view.ajax)]
#前端访问接口或浏览器打开时为http://127.0.0.1:8000/index/最后一个斜杠
#与urls文件同级的view.py文件中：

from django.http import HttpResponse,JsonResponse
import json
def hello(request):
    return JsonResponse('hello')
#当浏览器输入127.0.0.1:8000/index时就会触发ajax()函数
def ajax(request):#若有值传来则

```

渲染 web 模板如下：

```py
from django.shortcuts import render

def runoob(request):
    context = {}
    context['hello'] = 'Hello World!'
    return render(request, 'template/index.html', context)
```

<i class="label1">使用 docker 部署 django 项目</i>可以使用 apache 来部署 django 项目，但是经常遇到很多问题，而 docker 部署可以为每个项目单独建一个环境，将多个项目分开，非常便于维护(docker 的安装见 36)，而且使用 docker 来部署项目也会方便很多(只不过 windows 上 docker 的安装很多坑)。[docker 部署 django 教程。](https://blog.csdn.net/BlueBlueSkyZ/article/details/89083285)[Dockerfile 文件编写规则。](https://www.cnblogs.com/549294286/p/11044901.html)
<i class="label2">问题集</i>run server 时提示：DLL load filed》[该网站下载 sqlite.dll 放到环境的 DLLs 目录下。](https://sqlite.org/download.html)
<i class="label1">flask 的使用</i>pip install flask#安装 flask。pip install flask-cors

```py
from flask import Flask,request
from flask_cors import *
import json,os
AI = Flask(__name__)
CORS(AI,supports_credentials=True) #设置跨域

@AI.route('/ai/nlp/',methods=['POST','GET']) #methods可设置规定访问的方法。
def extract():
    mt = request.method #获取请求的方式。
    st = request.form['sentence'] if mt=='POST' else request.args.get('sentence',None) #获取参数
    return json.dumps({"status":200}) #返回的数据格式要用json封装。

# flask接受前台传来的文件
@AI.route('/file/',methods=['POST','GET'])
def fl():
    from werkzeug.utils import secure_filename
    #    前端直接传送一整个formdata数据过来。
    a = request.form.get('name')# 获取form表单中普通的数据，如type为text类型的输入框中的值。
    b = request.files['file']# 获取文件对象。file是input标签中指定的名。
    fname = secure_filename(b.filename)# 使用secure_filename()能获取到正确的文件名。
    if fname!=None:
        save_path = os.path.join('data',fname)
        b.save(save_path)# 直接调用save()方法保存文件。
        # 先保存好文件才能读取文件内容。使用完后可以用命令删除文件。
        with open(fname,'r') as f:
            for c in f:
                print(f)

if __name__=='__main__':
    #127.0.0.1才是测试地址，本地测试接口时使用。
    AI.run(host='127.0.0.1',port='8050')
```

<i  class="violet">传参注意：接口中使用到的参数都必须传，不然会直接报 404 错误，而不是找不到参数的错误，即使使用了判断要不要获取参数的情况(比如后台根据 typ 值为 0 则使用文本参数 text，否则使用获取文件参数 file，那么前端需要 3 个都上传，且 file 是文件类型，都要与后台对应)。，要求之外的参数，前端可以多传。</i>
[flask 使用教程。](https://www.cnblogs.com/klb561/p/8679320.html)[flask 的部署。](https://www.jianshu.com/p/5b09394bebfe)

### 6、服务端缓存：

将常被访问的数据放置于缓存器中（主存到 cpu 之间的缓存），提高反应速度。服务端语言也较易于控制缓存的释放。
**redis 缓存机制**：将内存数据在写入之后按照一定格式存储在磁盘文件中，宕机、断电后可以重启 redis 时**读取磁盘中文件恢复缓存数据**。
**Memcached**：是一种基于内存的 key-value 存储，用来存储小块的任意数据（字符串、对象）。这些数据可以是数据库调用、API 调用或者是页面渲染的结果。解决了大数据量缓存的很多问题。它的 API 兼容大部分流行的开发语言。本质上，它是一个简洁的 key-value 存储系统。
**CDN**：服务器是一种特殊类型的服务器系统，准确的说它不是一台服务器，而是由**多台服务器组成**的一个缓存服务器系统。它可以起到对互联网服务器加速的功能。通常来说我们的互联网服务都是部署在某地某一台服务器上，但是这个地方的网络在全国各地的访问速率是不一样的，远的地方或者线路不一样的地方，延迟可能会很高。采用 CDN 服务器后，由于在全国各地均有缓存服务器，系统能够根据用户位置提供距离客户最近的缓存服务器，所以能够大大减少延迟，提升网络服务器的访问速度。

### 7、python 时间：

```py
import datetime
from datetime import timedelta
import time
import calendar
tim1 = time.time()#一个时间戳，适合做计算支持1970-2038年之间
tod = datetime.datetime.today()#2019-06-29 15：23：57.514309，获取当前点时间
#datetime.today(),与timedelta结合查询最近几天时间
res=(datetime.today() + timedelta(days=1,hours=0)).strftime('%y-%m-%d')#表
#示查询1天后此刻的时间，再转为-格式。
tim2 = time.localtime(time.time())#时间戳转换了一种形式，但不能直接使用
tim3 = time.asctime(tim2)#/最简单的获取可读时间的方法
time4=time.strftime('%Y-%m-%d %H:%M:%S',time.localtime())#格式化时间按照
#指定的格式输出时间2019-5-18 11:30:27,%Y,%H...是属于时间的格式化字符串。
month = calendar.month(2018,10)#获取年份下某月份的日历表。
#strptime()将一个字符串时间转为程序识别的时间。
tt = datetime.datetime.strptime("2012-08-21", "%Y-%m-%d %H:%M:%S")# 不加时间的话会自动补为00:00:00
tm = datetime.datetime.strptime("2010-08-21", "%Y-%m-%d %H:%M:%S")
mq = (tt - tm).days    #时间转为int型。

# 计算几天后的日期：
s = time.sleep(5)
end = datetime.datetime.now()    #获取到的是5天后的世界。

def minNums(startTime, endTime):
    '''计算两个时间点之间的分钟数'''
    # 处理格式,加上秒位
    startTime1 = startTime + ':00'
    endTime1 = endTime + ':00'
    # 计算分钟数
    startTime2 = datetime.datetime.strptime(startTime1, "%Y-%m-%d %H:%M:%S")
    endTime2 = datetime.datetime.strptime(endTime1, "%Y-%m-%d %H:%M:%S")
    seconds = (endTime2 - startTime2).seconds
    # 来获取时间差中的秒数。注意，seconds获得的秒只是时间差中的小时、分钟和秒部分的和，并没有包含时间差的天数（既是两个时间点不是同一天，失效）
    total_seconds = (endTime2 - startTime2).total_seconds()
    # 来获取准确的时间差，并将时间差转换为秒
    print(total_seconds)
    mins = total_seconds / 60
    return int(mins)

if __name__ == "__main__":
    startTime_1 = '2019-07-28 00:00'
    endTime_1 = '2019-07-29 00:00'
    fenNum = minNums(startTime_1, endTime_1)
    print(fenNum)
```

**定时器**：

```py
from datetime import datetime
import time
def timer(n):
    while True:
        print(datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
        time.sleep(n)# sleep()是阻塞式的，期间不能做其它操作。
timer(5)# 每5秒执行一次

#--------- 另一种方法，sched实现一个通用事件调度器。
import sched

# 初始化sched模块的 scheduler 类
# 第一个参数是一个可以返回时间戳的函数，第二个参数可以在定时未到达之前阻塞。
schedule = sched.scheduler(time.time, time.sleep)
# 被周期性调度触发的函数
def printTime(inc):
    print(datetime.now().strftime("%Y-%m-%d %H:%M:%S"))
    schedule.enter(inc, 0, printTime, (inc,))
# 默认参数60s
def main(inc=60):
    # enter四个参数分别为：间隔时间、优先级（用于同时间到达的两个事件同时执行时定序）、被调用触发的函数，
    # 给该触发函数的参数（tuple形式）
    schedule.enter(0, 0, printTime, (inc,))
    schedule.run()
# 10s 输出一次
main(10)
```

### 8、python 读取文档：

csv 文件读取与存储:

```py
import csv
#读取
c = open('data.csv','r')
reader = csv.reader(c)
a = []
for f in reader:
    print(f)# 每列以列表形似呈现。
    if f == '\x00': # 提示存在null bytes时可这样跳过。
        continue
    a.append(f)
# 存储
with open('av.csv','w') as w:
    writer = csv.writer(w,delimiter=' ')#delimiter可以设置每列值之间使用的隔开符，默认是每个值占一格。
    writer.writerow(['id','name','val'])#写入一行。
    writer.writerows([[],[],[]]) #writerows()同时写入多行

[xml格式读取。](https://www.cnblogs.com/xiaobaixiaobai/p/10724829.html)
pip install python_docx #需要安装python_docx，安装docx的话是2版本的3中用不了。

# docx文档读取
from docx import Document
from docx.shared import Inches
document = Document('/home/wcs/data/人工智能.docx')
i = 0
for p in document.paragraphs:
    print(p.text) # 打印每行的文本内容。
    if i > 5:
        break
    i += 1
document.add_paragraph('net text',style="ListNumber") #添加新的内容。
document.save('/data/av.docx')

```

[pdf 的读取学习地址。](https://www.cnblogs.com/xiao-apple36/p/10496707.html) pip install pdfplumber #另一个读取 pdf 的库是 pdfminer 功能更强大，但没有这个易用。

```py
import pdfplumber
with pdfplumber.open("/home/wcs/data/vv.pdf") as pdf:
    # 逐行读取。
    for c in pdf.pages:
        print(c.extract_text())#读取每行的文本，还有其它函数：extract_words(),extract_tables(),extract_image()
```

xlsxwrite 模块，可用于自动化生成报表使用：

```py
import xlsxwriter

# 新建一个xlsx文件
book = xlsxwriter.Workbook(filename=u'员工统计表.xlsx',
   options={  # 全局设置
        'strings_to_numbers': True,  # str 类型数字转换为 int 数字
        'strings_to_urls': False,  # 自动识别超链接
        'constant_memory': False,  # 连续内存模式 (True 适用于大数据量输出)
        'default_format_properties': {
            'font_name': '微软雅黑',  # 字体. 默认值 "Arial"
            'font_size': 14,  # 字号. 默认值 11
            # 'bold': False,  # 字体加粗
            # 'border': 1,  # 单元格边框宽度. 默认值 0
            # 'align': 'left',  # 对齐方式
            # 'valign': 'vcenter',  # 垂直对齐方式
            # 'text_wrap': False,  # 单元格内是否自动换行
            # ...
        },
    })

# 单元格合并后居中
fmt = book.add_format({'align': 'center', 'valign': 'vcenter'})
# sheet.merge_range(x1, y1, x2, y2, value, cell_format=None)
sheet.merge_range(0, 0, 1, 10, 'hello', cell_format=fmt)# 合并(0,0)到(1,10)

# 文件中创建一个工作表
sheet = book.add_worksheet(u'基本信息')
sheet.set_column('A:A',20)# 设置第一列宽度。
sheet.write('A1','Hello')　　#在A1单元格写入hello
sheet.insert_image('C3','/root/test/2.png')# 插入图片

head = [u'姓名',u'出生日期',u'学历',u'身高']
names = [u'张三',u'李四',u'赵五',u'钱六',u'泰七']
learn = [u'博士',u'研究生',u'本科',u'专科',u'高中']
lens = [1.75,1.8,1.7,1.69,1.68,1.65]


sheet.write_column('A2',names) # 写入列
sheet.write_column('C2',learn)
# 也可以指定行，列索引来指定位置，1对应行号2.
sheet.write_column(1,1,['1991/6/23','1995/2/28','1997/9/21','1996/5/24','1992/7/30'])
sheet.write_column('D2',lens)

# 创建一个设置样式，格式的对象。在写入时使用
workfomat = sheet.add_format()
workfomat.set_bold(1)                #设置边框宽度
workfomat.set_num_format('0.00')     #格式化数据格式为小数点后两位
workfomat.set_align('center')        #设置对齐方式
workfomat.set_fg_color('blue')       #设置单元格背景颜色
workfomat.set_bg_color('red')         # 也是设置背景色

# 写入时，指定使用上面的format样式。
sheet.write_row('A1',data=head,cell_format=workfomat)# 写入一行，从指定位置开始，依次每格写入数组值


# 插入图表，
chart = book.add_chart({'type': 'column'})    #创建一个图表对象
#设置图表数据
chart.add_series({
    'categories':'=基本信息!$A$2:$A$6',
    'values':'=基本信息!$D$2:$D$6',
    'line':dict(color='blue',width=1),
    'name':'图1'
})
# 设置图表样式
chart.set_size({'width': 577, 'height': 287})            #设置图表大小
chart.set_title ({'name': u'员工身高'})          #设置图表(上方)大标题
chart.set_y_axis({'name': 'm'})         #设置y轴(左侧)小标题
chart.set_table() #设置x轴为数据表格式，对应的值展示在下方表格中。
sheet.insert_chart('G1', chart)

# 其它图表类型：id分别为1,2,...。可用chart.set_type(1)#这样来设置类型。
area：创建一个面积样式的图表；
bar：创建一个条形样式的图表；
column：创建一个柱形样式的图表；
line：创建一个线条样式的图表；
pie：创建一个饼图样式的图表；
scatter：创建一个散点样式的图表；
stock：创建一个股票样式的图表；
radar：创建一个雷达样式的图表

book.close()# 关闭文件。

```

[xlsxwrite 模块其它方法学习地址。](https://www.jianshu.com/p/9952293a4bb8)

### 9、后端身份验证：

1. 基于 cookie 的 session 验证：客户端浏览器访问服务端时，服务端都能获取到客户端 cookie 中的信息，以此来区分各用户。<b c=r>跨域访问时，获取不到对方浏览器中的 cookie</b>
2. token 鉴权机制：客户端登录时得到服务端的一个身份标识，客户端每次访问时可将其放与 http 头中，这样跨域访问，也是可行的。
3. JWT：Json web token 是为了在网络应用环境间传递声明而执行的一种基于 JSON 的开放标准，可实现无状态、分布式的 Web 应用授权。

10：panda3d
[官方文档](https://docs.panda3d.org/1.10/python/index)
[学习地址 1](https://zhuanlan.zhihu.com/p/268163358)

### 12、文件 IO：

假设当前路径为 E:\mypython\test\文件 IO.py。文件分为文本型和二进制型，所以读取的模式也只分为两种。(写入文件时需要保证写入的类型是字符串类型或 byte 型，不然非字符型会出现 output Decode utf-8 错误，不易查找)。部分特别的符号需要使用特别的编码才能实现，所以文件中有不同编码格式的字符时需要使用 rb 模式来读后再解码，不过解码后每个字符后还会有\r 符。
读取二进制型文件时需要对读取的结果解码，用如下方法查看文件的编码方式：

```py
import chardet
tf = open('dat.bin','rb').read()
print(chardet.detect(tf))#{'encoding':'utf-8','confidence':0.1,'language':}

open()函数所有参数：https://www.cnblogs.com/IMWU/p/10947262.html
fil = open('tt.txt','w')#w为只写模式一般文件是文本文档的格式,(原有内容被删)
fil = open('tt.txt','wb+')#wb+以一个二进制方式打开文件,写入的也必须是二进制
fil = open('tt.txt','r')# 只读模式,rb+为以一个二进制格式打开文件读写(图片)
fil=open('tt.txt','a','gb2312')#打开文本写入是追加模式，第三个参数为解码
fil=open('tt.txt','ab+',encoding='utf-8')#以二进制格式打开文件用于追加
fil.readline()#读取第一行，类似一个迭代器，一直运行会逐行读取
fil.readlines()#按行读取，返回每一行的文本,读取的每一行会
#带上\n符号，需要去除。(行是以\n结尾的为行)
fil.write(data)#写入文件，关闭文件前一直写入的话是追加的形式。
fil.writelines(list)#将一个列表写入，但不会自动加换行符。
```

OS 模块提供的文件 IO：

```py
import os
print(os.path.isfile('adr.txt'))#判断路径是否为一个文件，True或False
os.path.join('/mypython','test\wds.txt')#将路径与文件名结合,第一项后面，第二项前面都不要加/
os.rename('data/p1','data/av1')#对指定路径文件进行重命名
os.path.exists(file)#判断该文件是否存在。
os.path.splitext('file_name')#一个二元组(文件名，文件后缀名)
fad=os.open('w.txt',os.O_RDONLY|os.O_CREAT)//os.O_RDONLY表示只读,无则创建
#os.O_WRONLY(只写),os.O_RDWR(读写),os.O_CREAT(创建并打开)
os.read(fad,10)#10为读取的最大长度,要全部读取只能使用open()方法。

with open('a.txt','rb') as f:
    for i in f:#读取文件的每一行内容
        print(i.decode('gb2312'))
avt=os.getcwd()#获取当前目录一般类似 /mypython
os.chdir('/pscs6')#改变当前工作目录pscs6是与mython同一级的文件夹
ak = os.listdir('/mypython')#/获取目录下的所有目录及文件
for r,dirs,files in ak:
    print(r,dirs,files)#分别是当前目录下的所有一级目录，当前目录下的一级目录下
    #/的所有目录，当前路径下所有非目录的子文件
```

[获取文件属性]os.stat(file)#属性如下：
st_model:保护模式;st_ino:节点号;st_dev:驻留的设备;st_nlink:连接数;st_uid:所有者的用户 id;
st_gid:所有者的组 id;st_size:以字节为单位的文字大小;st_atime:上次访问的时间;st_mtime:最后一次修改的时间;
st_ctime:由操作系统报告的"ctime"。在某些系统上（如 Unix）是最新的元数据更改的时间，在其它系统上（如 Windows）是创建时间。
[复制文件]from shutil import copy ==>copy(a,b)#a 文件位置复制到 b 文件位置或 b 文件夹下
注：无论是使用 open()方法还是使用 OS 模块最初的目录状态是你进入编辑器时打开的那个目录（E:\mypython）...
进入当前目录下的一个子目录：os.chdir('/mypython/test')//os 模块 open()都适用选择目录下的一个文件：fc=os.open('test\wds.txt')//需要直接写 mypython 下的目录然后反斜杠选择其下的文件(坑爹的用法!),且如果 test 目录下还有其它 python 文件则会报错。
保险的方法读取当前工作目录下一个子目录中的文件：
有时 os.open('test\wds.txt',os.O_RDONLY)这样写会报找不到文件的错误。可以：

```py
import os
#改变工作区最好也用这种全路径拼接的方法
herePath = os.getcwd()#获取当前工作路径
dirs = os.listdir()#获取当前路径下所有一级子目录及文件

for i in dirs:
    if i=='test_batch':
        path = os.path.join(herePath,i)
        read_ = os.open(path,os.O_RDONLY)
       print(os.read(read_,100))#成功
os.walk('E:/obj',topdown=True)#遍历指定路径下文件目录反回一个三元组
#:(所有一级文件夹路径、所有一级文件、一级文件夹下所有文件名称)
os.stat('E:/obj')#获取目标路径下所有信息包括:保护模式、驻留设备...[有一个
#st_size属性为文件中数据的长度。]
os.path.basename(path)#返回文件名
```

获取、设置系统环境变量：

```py
os.system()：system()函数可以将传入的字符串转为在电脑上执行cmd命令，执行时会创建一个子进程，示例如下：
os.system('shutdown -s -t 60') #1分钟后关机
os.system("net start mysql") #开启mysql服务
os.environ//获取系统的环境变量，返回一个字典，所以可以用get()，[]等方法。
# 获取cpu核数,一般将线程数设置为核数-1。
os.cpu_count()
```

图片的存储与读取:(点击图片属性>尺寸显示的是宽 x 高，但程序获取的是[高,宽,通道数])

```py
from PIL import Image #python自带的一个读取图片的包
import tensorflow as tf
im = Image.open('av10.jpg')#PIL读入的图片数据需要先转为numpy型再转为张量才能
#被tensorflow使用
x = np.array(img)#使用numpy额array()可以将图片对象转为像素数据。
im.convert('LA')#将图片转为灰色(只右两个通道)
w,h = im.size()#获取图片的宽高
ig = im.resize((100,100))#将图片压缩到指定尺寸(最近邻插值)。
saveim = open('av10.bin','rb+')
img = im.tobytes()#将图片数据转换为原生byte型
saveim.write(img)#之后再用tensorflow中的读取器读取bin文件即可
#可用scipy下的ndimage模块读取到的图片直接是像素数据
dats = ndimage.imread('av.jpg')
```

https://blog.csdn.net/qq_38255689/article/details/78461398
https://blog.csdn.net/u014061630/article/details/80712635

### 19、对象类常用方法：

list = [];obj = {},arr = (),st = set()
**集合的使用**：若创建时有重复的元素则只会保留一个，可使用 len(),in,pop(),clear()方法
st = set()#创建空集合；set(('ac','vb))#传入一个 tuple/list 时每个值为集合值
st.update({1,3},[2,4])#{1,2,3,4}向集合中添加值,集合中不会有非数值和字符的数据
st.add('hello')#添加值
st.remove(1)#将值 1 移除,若值不存在会报错
st.discard(9)#移除值 9，若值不存在不会报错
b = {'a','b','c','v','m'}
集合间的运算
st - b#减掉同时包含的元素，剩下 st 中的元素
st | b#合集，两个个集合中的所有元素
st & b#交集，两个集合同时包含的元素
st ^ b#两个集合不同时包含的元素，交集的补集
**列表使用**：
**反转列表**：`c = x[::-1]`
min(list),max(list),len(list);#求列表的最小最大值和元素个数。sum([1,2,3])求一维列表的总和
list.append()#只能使用此方法在列表中添加新的值（末尾添加）
list[::2]#2 表示从第一个起每隔 1 个值就取一个值。
append()方法是按引用添加的而不是按值添加的，例：x = [],obj = {"a":1,"b":2}
x.append(obj),obj['a']=3,obj['b']=4,x.append(obj) ;结果：
x[obj,obj] >> x[{'a':3,'b':4},{'a':3,'b':4}];是按 obj 这个引用添加进去的。
list.extend(obj)//extend 方法在列表后添加一个列表
list.pop(2)#移除列表最后(默认)一个值，2 选择位置，返回删除的值，直接在原值上操作。
list.insert(index,obj)#向列表中插入值，位置，插入对象
list.index(obj)#查找值 obj 所在索引位置,若值不在列表中会报错
list.count(obj)#查看 obj 在列表中出现的次数,没有为 0，有 1 个则为 1
元组中的数据可以是任意，包括列表和字典，但元组中的数据不可更改
arr[0]#查询元组索引值为 0 处的值。
list.sort(reverse=True)//将列表排序，作用与原数据，默认从小到大排序。
list.reverse()#将列表中的元素反向排列。
list.remove(x)#移除列表中第一个与 x 匹配的值。
zip([1,2,3],[4,5,6]) >> [(1,4),(2,5),(3,6)]，
求和：sum(listData)#求出列表各值的总和。
**字典使用**：
`res=dict(zip(obj.keys(),obj.values()))`，`dict(a=1,b=2)`//将其创建为一个字典。dict([(a,2),(b,3)])>>{'a':2,'b':3}
obj.items()//将字典每对键值对封做一个
for 循环可迭代字典，不过迭代的是键值，for i in dict:
enumerate(list)#可枚举列表，元组，字典，for index,value in enumerate(list),注意：在枚举字典时得到的是索引和键，并不是键和值。
用 in 判断一个值是否在一个字典中是用该值与字典的键值名比较而不是依据 value 值
obj.get('age',None)#get()方法返回字典中指定键的值，第一个参数为键值名第二个参数规定键不存在时返回的值。obj.keys(),obj.values()#返回字典的键值和 value 值。obj.clearn()#清空字典
[sorted()排序字典]注意：第二个参数函数名必须用 key。返回按原数据格式排好序的结果
obj = {'a':10,'b':3,'c':16,'d':8}
移除元素：obj.pop('a','45')#移除键值为 a 的元素，第二个参数是若没有该键值返回的值，可赋给一个变量。
sorted()方法参数：要排序的数据,一个函数(会将每条数据传入这个函数),处理返回一个
值，内部会根据该值大小**排序**，默认从小到大。
`v = [t[0] for t in sorted(obj.items(),key=lambda k:abs(k[0]),reverse=True)]`#['c','a','d','b']
lambda 是一个简单构建函数的方法里面可以写一些简单的逻辑,后面跟一个 k 是函数参数。
第一个参数可以是任何可迭代的对象,第二个参数指定排序根据的属性,k 就表示 obj.items()//中每一个可迭代的对象。

```
Fruits = [‘banana’,  ‘apple’];
for fruit in Fruits:
    print(fruit);
for c,d in [['a',1],['b',2]]:
    obj[c] = d// {'a':1,'b':2}注意迭代的方向,不过zip()后迭代的方向不同
for (x,y) in zip(trainx,trainy):
    print(x,y)//一起迭代两个对象
```

// 若将 fruit 当做一个函数的参数传入函数中供 pandas,numpy 等库使用会报错
字典键值对反转：dat = dict(zip(obj.values(),obj.keys()))
对字典排序：sorted(obj)=>[3,8,10,16]
list[::2]//表示隔行取样,比如 list 是一个 5x3 的二维数组,读取的将是 0，2，4 行的数据。
数组中使用 for 循环：
a = [i for i in dat]#相当于循环得到的 i 逐个加入到数组中，i\*2,i[0],...可随意组合
map(function,[1,2,3])//map 方法是一个映射函数将第二个参数拿到第一个参数(函数)运行，第二个参数是一个字符串时传入函数的是每一个字符，得到的结果是一个迭代对象，可用 list 转为列表。
x = ['1','2','3']
s = list(mat(float,x))#将 x 中的每个值转为浮点型
sorted(a)//若 a 是一个列表则将其值按从小到大的顺序排序，若为字符则将其按字节大小英文字母顺序来排列，为字典则按键值来排。
obj.updata({'a':56})//如果原对象 obj 中存在键值 a 则更新其值，若不存在则将该键值对加入。

### 21、python 设计模式：

a1、前提基础：

```
hasattr(obj,'name') //对象obj中是否有name这个属性，如类Obj中是否有name这个变量值。
```

单例设计模式：

```py
class Single(object):
    def __new__(self):
        if not hasattr(self,'instance'):
            self.instance = super(Single,self).__new__(self)
        return self.instance
```

### 26、正则表达式：

`[0-9]`：表示匹配字符串中 0-9 的数字（包括 0 和 9），默认全局匹配,但是只返回找到的第一个。
`^[0-9]`：^号表示匹配以 0-9 数字开头的。
`^[0-9]+a`：要使用多个子规则匹配时使用+号连接，如 2a 就满足这个正则匹配结果。且加号前一个字符可以有多个(runo+b 可以匹配到 runoob,runooob...)
`runo?b`：?则代表？前一个字符最多只能出现 1 次，匹配 runob,runb
`[0-6]+yy$`：$符号表示以指定字符结尾的规则。如 aad0yy 满足该规则。
`[a-z0-9-_]{5,9}`：表示字符串中可以有 a-z 间的字母,0-9 间的数字及符号，长度在 5-9
匹配转义字符：\n(换行符),\r(回车符),\s(匹配任何空白符空格、回车...),\S(匹配任何非空白符)
匹配特殊字符：匹配字符串中的特殊字符时需要对正则式中的特殊字符转义如`+,*...变\+,\*`
限定符：`*,+,?,{n},{n,},{n,m}`。
**匹配特殊字符**：

```
[`~!@#$%^&*()_\-+=<>?:"{}|,.\/;'\\[\]·~！@#￥%……&*（）——\-+={}|《》？：“”【】、；‘'，。、]
```

`*`：匹配前后的子表达式 0 次或多次，如`wc*s`可匹配到 ws,wcs,cs,s，wcswcs...
()：可以将要匹配的字符用()包含，`ac*(abc)`匹配 acabc
`{n}`：匹配前一个字符多个(连在一起的情况),如：a{2}可匹配 chaa,与()一起使用：(ab){2}匹配 jabab，
列如：^1{1}[0-9]{10}匹配电话号码格式。
`{n,}`：表示至少匹配前一个字符 n 次，不过要求 n 时一个非负整数。
.：表示一个任意字符,如 a.b 匹配 acb 得到 cvg
`{n,m}`：n 和 m 均为非负数且 m>n
[]：[]内可以匹配多个字符如[abc]n 可匹配到 an,bm,cn。[0-9]表示可以是 0-9 内的任一个数字
贪婪：`<.*>`匹配`<abc><dv>`得到 abc,dv。`.*`组合匹配字符串中所有满足模式的字符。
非贪婪：在贪婪模式后加?符只匹配第一个满足规则的。
`\b`：边界匹配符(与控格相连的字符)，如\ba\b 匹配到'jk a op'中的 a，注意在 python 正则中使用时会被当做回退符被忽略解决办法使用 r 进行转译：re.search(r'\btc\b','j btc op')//\b 放单边也行
`\B`：非边界匹配符，只匹配不与空格相连的字符。
`\W`：匹配非字母、数字、下划线、中文。如'\W'匹配'kc*&op78'得到&。等价于'[^A-Za-z0-9*]'
`\w`：匹配字母、数字、下划线、中文。等价于'[A-Za-z0-9_]'
`\d`：匹配一个数字字符。等价于[0-9]
`\D`：匹配一个非数字字符。
`[^0-5]`：赋值字符串，在[]中第一项加^表示取中括号中范围外的值。
`|`：或字符，如 a|b 表示匹配 a 或 b。
**精准匹配**：`^abc$`
**匹配中文**：`[\u4e00-\u9fa5]+`表示匹配所有中文。(只要有中文就能匹配成功)
**全部为中文**：`^[\u4e00-\u9fa5]+$`必须全部为中文。
**全部为同一类型的写法**：先表示好一个匹配的规则，然后开头加`^`，最后加`+$`。
所有转义字符：\a:响铃(BEL) \b:退格(BS) \f:换页(FF) \n:换行 \r:回车
`\t`:水平制表(HT)table 符 \v：垂直制表(VT) \o:空字符 \s：空格

```js
// 检验邮箱号
var a = /^\w+@\w+([-]\w+)*(\.\w+)+$/;
// 检验身份证号
const _r =
  /^[1-9]\d{5}(18|19|20)\d{2}((0[1-9])|(1[0-2]))(([0-2][1-9])|10|20|30|31)\d{3}[0-9Xx]$/;
// 手机号
var c = /^1[0-9]{10}/;
```

### 27、python 知识积累：

python 并非完全是解释性语言，它是有编译的，先把源码 py 文件编译成 pyc 或者 pyo，然后由 python 的虚拟机执行，相对于 py 文件来说，编译成 pyc 和 pyo 本质上和 py 没有太大区别，只是对于这个模块的加载速度提高了，并没有提高代码的执行速度，通常情况下不用主动去编译 pyc 文件。ython 和 Java/C#一样，也是一门基于虚拟机的语言，当我们在命令行中输入 python hello.py 时，其实是激活了 Python 的“解释器”。可是在“解释”之前，其实执行的第一项工作和 Java 一样，交由虚拟机执行：(1)完成模块的加载和链接、(2)编译，即将源码转换为 PyCodeObject(字节码)。(3)从上述内存空间中读取指令并执行、(4)程序结束后，根据命令行调用情况（即运行程序的方式）决定是否将 PyCodeObject 写回硬盘当中（也就是直接复制到 .pyc 或 .pyo 文件中）。(5)之后若再次执行该脚本，则先检查本地是否有上述字节码文件。有则执行，否则重复上述步骤。

计算机是不能够识别高级语言的，所以当我们运行一个高级语言程序的时候，就需要一个“翻译机”来从事把高级语言转变成计算机能读懂的机器语言的过程。这个过程分成两类，第一种是编译，第二种是解释。
编译型语言在程序执行之前，先会通过编译器对程序执行一个编译的过程，把程序转变成机器语言。运行时就不需要翻译，而直接执行就可以了。最典型的例子就是 C 语言。
解释型语言就没有这个编译的过程，而是在程序运行的时候，通过解释器对程序逐行作出解释，然后直接运行，最典型的例子是 Ruby。

生成 pyc 或 pyo 文件：.pyo 是更优化的编译，比.pyc 略小。[参考学习地址。](https://blog.csdn.net/chinesehuazhou2/article/details/105236390)

```
python -m py_compile /path/to/需要生成.pyc的脚本.py
# 或
import py_compile
py_compile.compile(r'/path/to/需要生成.pyc的脚本.py')
# 生成pyo
python -O -m py_compile /path/to/需要生成.pyo的脚本.py
```

在编写 python 程序时开头使用# -_-coding:utf-8-_-用于规定使用的字符集编码,这 样程序注释中可以使用中文，#!/usr/bin/python 规定使用 python 解析器解析程序。
frozenset(range(10))//创建一个不可变集，frozenset('thisisaman')//返回：
frozenset({'s', 'h', 'm', 'a', 'n', 't', 'i'})；set(range(5))//创建一个可变集。
双斜杠运算符, // 表示取整除部分(向上取整)

#### a1、collections 模块

```
from collections import Counter,OrderedDict
print(Counter('string'))//将字符串转换为一个字典,以每个字符为键，以其出现次数为值。若目标对象是一个列表则是一个一维数组时才能使用Counter()方法。
Counter('str').most_common(2)//Counter()对象下的方法得到出现数最大的前两组。
import random
lv = [1,2,3,4,5]
print(Counter(lv))# 统计列表中各元素出现的次数。
'+'.join(lv)#将数组各个数之间用+号连接。
random.shuffle(lv)#打乱数组List中值的顺序,但并不返回一个打乱后的结果
print(lv)#[3,1,5,4,2]
#非运算：if not (y=20):print('ok')
#OrderedDict也是一个字典，不过里面存储会按添加的顺序来顺序存储，而普通字典不一定
d = OrderedDict()
for c,n in d.items():
```

#### a2、数据类型转换

int('8'),str(12),eval("1+2")//转为整型、字符串、可执行的 python 语句
float(1),ord("w")//转为浮点型、反回对应的 ASCII 码(同时只能转一个长度字符串)
hex(10),oct(10)//返回对应的 16 进制，8 进制。
b'123',bytes('string')//变为 byte 型,(字符串可被编码为字节,字节可解码为字符串)
string.endswith('.av')//判断字符是否以.av 结尾，返回布尔值。
string.strip('0')//删除字符串首尾所有满足条件的字符,如果是 byte 型则条件也要加上
byte 型【string.strip(b'0')】
string.split('avbnvmk'.split('v',1))//将字符串以第 1 个 v 开始分割['a',bnvmk'']
string.count('i')//反回子字符串在 string 中出现的次数。
对列表进行排序时直接 x.sort(),x = x.sort()会被置为 None 因为 sort()方法不返回值
编码：'wcs'.encode(encoding='utf-8') >> b'wcs'
解码：b'wcs'.decode(encoding='utf-8') >> wcs。[python 中的字符集有：gbk,utf-8,
gb2312,ascii]
触发异常:if not s:#not 是非运算,raise 抛出异常,后面是异常名,括号内是输出的内容
raise ValueError('s is not false')#后面的代码会终止运行
**import**('a')//动态导入 a.py 模块，如果导入的类，函数是经常变化的情况

#### a3、字符串

b'xx08eu'(字符串前加 b 表示是一个 byte 类型)，r'e:\b\d'(字符串前加 r 表示去掉反斜杆的影响)。
u'字符'(字符串前加 u 表示使用 unicode[utf-8]进行编码，中文使用)。f"zzr{name}ko"，字符串前加 f 后该字符串中可以用{}号然后里面写变量名。

- **格式化字符串**：
  `print('a is s% and %d c'%('b',20))>'a is b and 20 c' `//%s 和%d 相当与占位符把%后的元组依次写入站位符中。
  `%s,%d,%c,%o,%x,%f...`分别表示占位字符串、整数、字符及 ASCII 码、八进制数、十六进制数，浮点数。
  字符串前使用 r 或 R 可以输出原始字符串：r'\n,%s,uio',里面的特殊字符不会被转译。'%(name)s--%(age)d'%{'name':'wcs','age':21}
  保留两位小数：使用 round()不生效的时候可以："%.2f"%number
- cv = x.replace('二',1)#替换 x 中为二的字符串为 1，返回一个结果，不在原结果上修改
- 'str'.find('t')//匹配字符串中所包含的指定子字符的第一次出现位置有则返回位置无则返回-1
- **类型转换**：可以直接转换一个数组的所有值：str(list)。[学习地址。](https://www.runoob.com/python/python-strings.html)
- **空字符串判断**：`string.isalnum()`#如果 string 至少有一个字符并且所有字符都是字母或数字则返回 True,否则返回 False。还有很多其他字符串操作函数。
- **join()的使用**：

```py
c = '-'.join(('a','b'))#将列表或元组用指定字符连接，如果列表值为数值型要转str
txt.strip('\n')//删除字符串中的转行符，rstrip(),lstrip()删除左右的，string.replace('a','s')//将string字符串中的a全部替换为s。
[startswith()]str.startswith(str, beg=0,end=len(string));检查字符串是否以指定字符开头，beg，end指定检查的起始和结束位置。
[format格式化函数]使用方法与格式化字符串类似：(与字符串连接使用)
print("name is {0},age is {1}".format('w',22))#{}内传索引时指定顺序
print("{0},{1},{0}").format('a','b')
print("{name},{age}".format(name='wcs',age=22))#指定键值
```

**条件赋值简写**：tag = 10 if tag>15 else 20
使用 with 同时打开多个操作：用逗号隔开，换行写时加上\号。

```
with open('data/train.txt','w') as data_a,\
    open('data/test.txt','a') as data_b,open('c.txt','r') as c:
    print(data_a.read())
```

#### a4、sys 模块

[一个详解教程](https://www.cnblogs.com/fmgao-technology/p/9074282.html)

```py
import sys
sys.argv[0]#实现从程序外部向程序传递参数。
print(sys.maxunicode)#查看python内部使用的编码，1114111就是UCS-4编码，65535就是UCS-2
sys.path.append("/home/wcs/ITEM") #改变但前文件的运行位置，但是os.getcwd()不会改变。

#输入输出
a = sys.stdin.readline().rstrip()
b = sys.stdout.write(a)
```

#### a5、codecs 模块

python 的内部是使用 unicode 来处理的，但是 unicode 的使用需要考虑的是它的编码格式有两种，一是 UCS-2，它一共有 65536 个码 位，另一种是 UCS-4，它有 2147483648g 个码位。对于这两种格式，python 都是支持的。import codecs

```py
look1 = codecs.lookup('gb2312')#创建编码器，传入类型。
a = look1.encode('中文')#对str类型编码
b = look1.decode(a)#对bytes类型解码
#codecs模块自带的open()方法在读取文件时按指定编码类型解码数据。
file = codecs.open('data/words.txt','r','gb2312')
print(file.read())
```

#### a6、迭代器与生成器

举例，如果我们想要自己实现一个和 range()函数一样功能的函数可能会使用循环来生成一个列表然后返回该列表来实现，但当要生产的列表非常长时这会非常占用内存，更有效的解决办法是让其变成一个迭代对象(一种惰性获取数据项的方式：可理解为先记录要生产的列表长度，然后在使用其值时才会去生成对应的那个值，这样就解决了占用内存的问题)，所以在用 print()打印出来时，列表直接时一串值，而迭代对像是一个(iterable(i=10))之类的信息。python 中使用 yield 实现：

```py
#------迭代器
ak = [1,2,3]
bn = iter(ak) # 将ak作为迭代对象。

#-----生成器
def self_range(x):
    i = 0
    while i<x:
        yield i
        i += 1
    #在赋值给一个变量时不会运行，获取所有迭代值后才运行这里
    print('err')

yd = self_range(5)
for n in yd:
    print(n)#0,1,2,3,4

#----读取
item = next(bn) #next(yd)，iter和yield作用的迭代器都可用循环和next()函数一条条读取。
```

注意：如果将该迭代赋值给一个变量则智能执行一个完整迭代(迭代完后失效)

#### a7、装饰器@

```py
def log(func):#会先运行log函数再运行test函数
    print('enter log')
    func()
    def back():
        return 20
    return back#被@修饰的函数必须返回一个函数
@log#@修饰一个函数将下一个函数test作为log的参数
def test():
    print('test')
```

test()#若不运行 test 函数也不会运行 log 函数
类中使用的@property：

```py
class animale(object):
    @property#为避免类中的公共变量被随意修改，使用@property和函数
    def weight(self):#配合才能修改，确保一定安全
        return self.aw
#函数上加了@property后这个函数就成了@property的一个实例，
#下面才能使用@weight
    @weight.setter#还有.deleter
    def height(self,inp):
        self.aw = inp
dog = animale()
print(dog.weight)#直接获取其值
dog.weight = 15#其实改变的是aw的值。若是改变一个列表or字典的值可
#改为dog.list=('a',12);修饰符内:self._val[arg[0]]=arg[1]形式
```

#### a8、json 与 字典互转

```py
import json
dat = open("dat.json","r")
dat = dat.read()#获取json文件中的数据
res = json.loads(dat)#将json转为字典
x = json.dumps(res)#将字典转为json对象
#当数据中有自己定义的类如numpy时，json不能将其序列化存储，可以：
class DecimalEncoder(json.JSONEncoder):#似乎无效，以后研究
	def default(self,o):
		if isinstance(o,decimal.Decimal):
			for i,j in enumerate(o):
				o[i] = list(j)
			return list(o)
		super(DecimalEncoder,self).default(o)
```

#### a9、piclke 模块的使用

pickle 类似于 json 的使用，pickle 也是用于序列化的模块，不过 pickle 用于 python 特有的类型和 python 数据类型间进行转换。

```py
import pickle
obj = ['a','b',1]
with open('k.txt','wb') as file:
#dump将数据obj转换为byte型,写入文件,file为文件对象,必须以二进制模式打开,若不
#传入文件对象则不写入文件，返回序列化后的数据，protocol为协议
    pickle.dump(obj,file,protocol=None)
#以二进制打开文件后用load导入，file一样是文件对象
    ag = pickle.load(file,encoding='ascii',errors='strict')
```

#### b1、杂项：

**math 模块**：

```py
import math
x = math.floor(2.3)#2 下舍
x = math.ceil(2.3)#3 上舍
```

**lambda 的使用**：lambda 用于构成一个简单的函数：h = lambda x,y:x+y#x,y 为参数，返回引号后的结果。
**callable()函数**：判断一个对象是否是可调用()函数。if callable(fun):#若 fun 是一个函数的话则返回 True
[argparse 模块]https://www.cnblogs.com/dengtou/p/8413609.html
[tqdm]tqdm 模块可以在循环体中显示进度。(非 python 自带模块，需要 pip install tqdm)

```py
from tqdm import tqdm
for i in tqdm(range(1314520)):#套在一个迭代器外使用即可
    print('zz')
```

[Decode error - output not utf-8]**错误解决**：python 默认使用的编码方式一般是 cp936 而文件一般使用的编码是 utf-8，在运行中解析非英文型字符时就会报这种错误，一些编辑器对此问题做了处理所以不会报错，而一些编辑器未做处理时就有这样的错误，解决如下：

```py
import sys,io
sys.stdout=io.TextIOWrapper(sys.stdout.buffer,encoding='utf-8')
```

**编解码器模块**：https://yiyibooks.cn/xx/python_352/library/codecs.html#module-codecs https://www.cnblogs.com/misswangxing/p/8603529.html \***\*future**模块**：把下一个版本的功能导入到这个版本测试使用。
**PIL 模块**：https://www.cnblogs.com/moying-wq/p/10982135.html
**any() 函数\*\*：用于判断给定的可迭代参数 iterable 是否全部为 False，则返回 False，如果有一个为 True，则返回 True。元素除了是 0、空、FALSE 外都算 TRUE。

#### b2、random 模块

```py
import random
a = random.random()#随机生成一个在0-1之间的数
b = random.uniform(1,10)#随机生成指定范围内的浮点数
c = random.randint(1,10)#随机生成指定范围内的整数
d = random.randrange(1,10,2)#相当于从[1,3,5,...,9]中随机选一个数
e = random.choice('l love math')#math,向指定序列(list,tuple等)中随机选一个
f = random.shuffle([1,2,3])#打乱指定序列顺序，作用于原始序列，不返回值
g = random.sample(lst,3)#向lst中随机选取3个数
```

#### b3、python 正则

在匹配函数后加.span()获得索引值，加 group()获得匹配结果

```py
import re
#compile()创建一个正则模式,参数为正则规则,第二个参数为匹配模式，
#re.l表示忽略大小写,re.M(多行模式),re.X(忽略空格和#后面的注释)
r = re.compile(r'*c$',re.l)

s = re.search(reg,'qq68786476号哈哈')#查找符合规则的第一个位置及返回结果。
v = r.search('fdjsklfd')
s.group()#qq68786476,查找结果为None的话则会报错。
s1=re.sub(reg,'替换值','qq26号string')#替换符合规则的字符串
s2=re.match(reg,'string')#只匹配字符串的开头，没有则失败。
```

#### b4、程序调试方法

1、断点打印：怀疑会出错的地方用 print()输出，太 low！
2、assert 断言：assert a==0,'a 不等于 0' //不满足 a==0 的话就会在控制台打印逗号后的字符串，且中断后面的代码。(与 print 一样，程序太大时也不建议使用)。
3、日志 logging：使用时需要导入 import
logger = logging.getLogger()
logging.basicConfig(level=logging.INFO)
logger.info('open file')#用 basicConfig 设置 level 为 INFO 后该信息能打印出来。
其它日志等级：
FATAL：致命错误
CRITICAL：特别糟糕的事情，如内存耗尽、磁盘空间为空，一般很少使用
ERROR：发生错误时，如 IO 操作失败或者连接问题
WARNING：发生很重要的事件，但是并不是错误时，如用户登录密码错误
INFO：处理请求或者状态变化等日常事务
DEBUG：调试
4、pdb 调试：import pdb 然后在想设置断点的地方 pdb.set_trace()，运行时会在此处停止，控制台出现(pdb)输入 n 运行下一步。
5，raise:显示的触发异常，直接抛出指定异常，停止运行后面的代码
if a==None:
raise ValueError('this value is None')#错误类型和详细提示。[常见 Error 类型。](https://www.cnblogs.com/zln1021/p/6106185.html)
https://blog.csdn.net/qq_38542085/article/details/78562458

#### b5、数据类型判断

使用 type(data)来获取数据的类型，使用 isinstance(data,cla)判断是哪一类型：

```py
v = (1,2,3,4,5)
if isinstance(v,tuple):print('is tuple')
if isinstance(v,list):print('is list')
if isinstance(v,dict):print('is dict')
if isinstance(v,int):print('is int')
if isinstance(v,np.ndarray):
#也可以使用type()
if(type(v)==tuple):
    print('this is a tuple')
```

Python 中使用 del 进行垃圾回收，将不用的对象销毁。
数据类型转换：`int("6",32)`#字符串转整型。`float(3);float('5.5')`#转浮点型。`str(4)`#转串。

#### b6、requests 模块的使用：

```py
import requests
url = 'http://localhost:8080'
r = requests.get(url)#get(),post()对应请求的方式，其它请求方式也类似这样使用。如：put(),delete(),head()...
#data是要传送的数据，params可以将键值拼在url上一起发送
r1 = requests.post(url,data={"txt":'hello'},params={"key":'val1',"key2":[0,1]})
print(r1.url)#编码后的url
print(r1.text,r1.json,r1.content)#text是网页结构内容，json是解析后的数据，content文数据的二进制形式。
```

[requests 模块的使用。](https://blog.csdn.net/lmz_lmz/article/details/83864863)

#### b7、深浅拷贝：

浅拷贝：数据完全共享

```py
a = [1,2,3]
b = a#改变b的值也会改变a的值，字典也是如此
```

浅拷贝：数据半共享

```py
# 其它的python数据结构都有copy()功能。
a = [[2,3,4],[5,6,7],7,8,9]
b = a.copy()#内部多层子数组是共享的，第一层的7,8,9是不共享的。
```

深拷贝：完全不共享

```py
import copy
a = [1,[2,3,4]]
b = copy.deepcopy(a)
```

#### b8、实现排列组合：

```py
import itertools
print(list(itertools.combinations([1,2,3,4],2)))#组合，无顺序限制
list(itertools.permutations([1,2,3,4],2))#排列
```

嵌套函数修改其主函数的变量：

```py
def a():
    mm = 1
    def b():
        nonlocal mm    #导入主函数的mm变量，否则下面报错
        mm += 1
        print(mm)
    b()
```

#### b9、异常检测：

```py
try:
    prt('vv')
except IndexError as e:
    print('---->', e)
    # except后面写上异常类型时可以列举多个。不写异常类型时只能用一个。
except KeyError as e:
    print(e)
else:    # 可以和else一起用。
    print('else')
finally:    #无论上面是进入了try还是进入了except,最后都会再执行finally下的语句。
    print('不管被检测的代码块有没有发生异常都会执行')

```

**PEP**:
PEP 的全称是 Python Enhancement Proposals，其中 Enhancement 是增强改进的意思，Proposals 则可译为提案或建议书，比较常见的翻译是 Python 增强提案或 Python 改进建议书。
[pep 提案地址](https://www.python.org/dev/peps/pep-0020/%20) 。[pep 简介地址，需看。](https://www.cnblogs.com/abella/p/10056875.html)
**help()和 dir()**:
dir()用来查询一个类或者对象所有属性，比如：
help()帮助查看类型详细信息，包含类的创建方式、属性、方法

```py
help(pandas)
dir(list)
```

**operator 模块**：
operator 模块是一些实现和 python 自带的计算方法，如加、减、异或运算、包含等操作，不过该模块使用 c 语言实现的，运算速度比 python 快。[参考学习地址。](https://www.cnblogs.com/who-care/p/9839058.html)
**打包为 exe 文件**：pip install pyinstaller。对要打包的文件进行：pyinstaller -F target.py#对应目录下出现一个 dist 目录，里面有编译装载链接后的文件。

### 34、python 多线程和锁:

一个程序可以有多个进程,一个进程可以有多个线程这与 js 的异步执行是一样的，Python2 中使用 thread 模块，在 python3 中废弃，使用\_thread 和 threading 模块，这里记录 threading 模块的使用。

```py
import threading
arr = []
class c_thread(threading.Thread):#继承threading中的Thread类
    def __init__(self,id,name,value):
        self.ID = id
        self.NAME = name
        self.VALUE = value
    def run():#会自动运行run()函数，应该与Thread类内部设置有关
        print(self.NAME+'start')#线程开始运行
       function()#要执行的操作
       print(self.NAME+'end')#结束
#创建两个线程
td1 = c_thread(1,'td1',1)
td2 = c_thread(2,'td2',2)
td1.start()#开启线程
td1.join()#等待开启的所有线程结束，一些需要等到所有线程结束的操作写在这步后面即可。
```

虽然是多线程不过在计算的数据量不大时还是几乎会看到一个线程运行的结束了另一个才开始这种效果，因为计算机的运行速度很快的原因。如果多个线程都操作一个共同的变量可能产生的结果并不是我们想要的(例如:我们运行一段代码看结果是否要继续之后的操)。<i class="blue">所以引入了锁的概念(这也叫线程同步)，锁有两个状态：锁定和未锁定</i>，当第一个线程访问到共享变量时获得锁定，操作完共享变量后结束锁定，如果该操作期间有其它线程也运行到访问该变量则让该线程挂起，即同步阻塞,实现如下：

```py
lock = threading.Lock()#创建锁
#run()函数中如下
lock.acquire()#运行到此处的线程获得锁定
function()#执行的操作
lock.release()#释放锁，让下一个线程进入。
```

<i class="blue">线程优先级队列 Queue</i>，Queue 模块提供了同步的、安全的队列类：

```py
import queue
q = queue.Queue(10)#创建先进先出队列，10个
q.put(1)#填充数据
a = q.get()#获取数据，一次取一个
#后进先出队列,使用与上一个一样
q2 = queue.LifoQueue()
```

Queue.qsize()#返回队列大小，Queue.empty()#判断队列是否为空，Queue.join()#等队列为空再执行其它操作。
https://blog.csdn.net/hellenlee22/article/details/91047807

### 62、python 发送邮件：

准备工作：指定的发送邮箱需要开启 SMTP 服务，进入电脑版邮箱中点击设置>用户选项，滚到下方点击开启 POP3/SMTP 服务，点击后按提示发送短信开启并获得第三方登录授权码。（SMTP 协议将邮件内容转码为机器码进行发送，接受端有 pop3 协议进行解码为人类可识别编码方式）。

```py
from email.mime.text import MIMEText    #导入邮件模块
import smtplib  #导入smtp协议模块
from email.header import Header
message = MIMEText('content','plain','utf-8')  #MIMEText()方法配置邮件参数，第一
个参数为邮件内容，第二个参数为邮件类型,plain:简单，第三个设置字符集.
message['From'] = Header("吴呈师",'utf-8')#发件人项处显示
message['To'] = Header('测试','utf-8')#收件人项显示
message['subject'] = Header('nice','utf-8') #邮件标题
 # 以上的 message中的设置发件人，收件人，标题时，里面的对象名一定要用From,To,subject;并且调用Header()方法才行
 # SMTP()方法调用SMTP服务，第一个参数为服务地址:smtp.qq.com;第二个参数为服务端口号默认25，第三个为主机名(可不填)。
server = smtplib.SMTP(server_add,port,hostname)
#login()方法登录，第一个参数为发送者邮箱，第二个参数为授权码(使用python操作是属于第三方登录所以不能使用密码只能使用授权码(授权码无空格))。
server.login(from,password)
#使用sendmail()方法开始发送邮件，to(收件者换位一个数组时可发送多个),参数为发送者邮箱、收件者邮箱、信息，as_string()方法将其转换为
server.sendmail(from,to,message.as_string())字符串。(可同时发送给多个人)。
#[我的邮箱登录授权码]mdmiylsovcthdjfd
server.set_debuglevel(1)#set_debuglevel(1)打印相关信息
server.quit()#退出服务;如下图：
```

![](_v_images/20200228140233665_838760176.png)

