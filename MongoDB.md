# MongoDB 常用命令

- 服务：mongod；
- 链接数据库：mongo；
- 查看存在数据库命令：show dbs；
- 查看数据库版本命令：db.version( )；
- 显示数据库中的集合（关系型中叫表，我们要逐渐熟悉）：show collections；
- 进入数据库（建立数据库）：use 集合名；存在则进入，不存在则新建；
- 显示当前位置：db；
- 新建数据集合和插入文件（数据）：db.集合名.insert( )；
- 查询所有数据：db.集合.find( )；
- 查询第一个文件数据：db.集合.findOne( )；
- 修改文件数据：db.集合.update({查询},{修改})；
- 删除文件数据：db.集合.remove(条件)；
- 删除整个集合：db.集合.drop( )；
- 删除整个数据库（在删除库时，一定要先进入数据库，然后再删除）：db.dropDatabase( )；
- 批量插入数据：mongo demo.js/load("./demo.js");
