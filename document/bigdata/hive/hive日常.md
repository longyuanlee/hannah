##hive 日常
INSERT OVERWRITE TABLE cgame.game_ad_ref_mapping 
select t.* from
(SELECT r.node_id, r.node_name , reference as ref FROM zhgame.goa_ad_ref r  lateral view explode(split(r.ref,',')) t as reference where dt=20170313 and r.ref != '' and r.ref is not null and reference != '' and reference is not null) t 
left join
cgame.game_ad_ref_mapping m  on t.ref = m.ref where m.ref is null;


##(Note: INSERT INTO syntax is only available starting in version 0.8.0)
1、INSERT OVERWRITE 和 INSERT INTO注意点
对于不分区的表
INSERT OVERWRITE 会覆盖掉表里面所有的数据，而并不是重复的那条数据。
INSERT OVERWRITE TABLE table1 IF NOT EXISTS (SELECT ***) 这种写法 IF NOT EXISTS没有作用的，还是会覆盖掉

对于分区的表
INSERT OVERWRITE 只会覆盖掉其所在的分区。

2、hive在版本xx不支持 not in 写法，在hivexx版本后支持。

3、hive 不支持不等值连接 

4、lateral view explode 和split结合用法（将数据分行）
SELECT r.node_id, r.node_name , reference as ref FROM zhgame.goa_ad_ref r  lateral view explode(split(r.ref,',')) t as reference where dt=20170313

5、hive不支持记录级别的更新、删除、插入

6、为什么要用hive？hive有什么特点？
hive最适合于数据仓库程序。（不需要实时响应查询，不需要记录级别的插入、更新、删除）


7、hive结构
(1)、hive包含cli以及可通过JDBC、ODBC、thrift服务器进行编程访问的几个模块
(2)、Driver模块。所有的查询和命令都会进入drive模块。--》该模块对输入进行解析编译。对需求的计算进行优化、再按指定的步骤执行（启动多个MapReduce任务）。
(3)、hive不会生成mapreduce算法程序，而是通过一个xml文件驱动执行内置的、原生的Mapper和Reduce模块。
(4)hive--jobTracker -->mapreduce

8、hive
有时候我们有些数据上传到数据库上格式不符合我们的要求，我们可以通过正则表达式来过滤这些数据，如一个int的数据，设计的时候用了string，这时候我们可以通过正则表达式来规避
    select giftid,giftname,giftdec,gameid,server,props,giftnum,mutexids,starttime,endtime,joinnum,exchangenum,rolescope,giftgroupid from cgame.gamegift_gift_package  where giftnum regexp "^([1-9][0-9]*)$" or giftnum = "";
    
9、hive现阶段只支持UNION ALL（即不消除重复记录）,不支持union。

10、hive里面substring的index表示0和1都表示从第一位开始。

11、编写hive
如果表使用了别名，那么字段全部要用别名。
连表查询先过滤条件再连表。
查询分区数据的，如果有两个分区，建议第二个分区应该指明。




    




