### MongoDB学习笔记

1. 安装地址：https://www.mongodb.com/download-center/community
2. 安装后在C盘创建data\db目录
3. 配置环境变量
  此电脑-》属性-》高级系统设置-》高级-》环境变量-》找到path-》编辑-》新建-》填入mongo安装的bin目录-》命令行运行'mongo'
4. 运行mongo命令默认连接的是test库
5. admin: root数据库，此数据库的用户自动继承所有数据库的权限；local数据库的数据永远不会被复制；config数据库在mongo分片设置时用于保存分片信息
6. capped collections：固定大小的集合，按照数据的插入顺序保存，在磁盘中也是按照插入顺序存放
7. 常用基础命令
  ```
  // 显示所有数据库列表
  show dbs
  // 切换、创建数据库
  use tangjj
  // 显示当前数据库
  db
  // 插入数据(只有往数据库中插入数据才算是真正创建了数据库)，在 MongoDB 中，你不需要创建集合。当你插入一些文档时，MongoDB 会自动创建集合
  db.tangjj.insert({"name": "隔壁小花"})
  // 删除数据库
  db.dropDatabase();
  // 创建集合
  db.createCollection('list')
  // 显示集合
  show tables或show collections
  // 删除集合
  // db.list.drop()
  
  ```

