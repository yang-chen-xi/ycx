# 复习

+ 路由参数后不带? , 请求资源路径后带?

+ postman模拟请求工具.提交表单时是post请求

+ 蓝图的名字是Blueprint后面的第一个参数

+ ```
  # flask-script flask-blueprint flask-session flask-sqlalchemy
  ```

# 笔记

数据库的环境

+ 开发环境----假数据           develop
+ 测试环境----数据量大一些,假数据        test
+ 演示环境----接近线上环境     实施工程师干的        show
+  线上环境----真实数据       product

# 学习目标

+ 项目拆分
+ flask-migrate
+ DML
  + 增删改
+ DQL
  + 查:
    + 获取单个数据
    + 获取结果集
    + 数据筛选
    + 分页
    + 逻辑运算



# 学习课程

### 1.项目拆分

```
数据库的环境
- 开发环境----假数据           			develop
- 测试环境----数据量大一些,假数据        	test
- 演示环境----接近线上环境,实施工程师干的      show
- 线上环境----真实数据      		 		product

拆分项目
	manager.py
		app的创建
        Manager （flask-script管理对象）
	App
        __init__
            创建Flask对象
            加载settings文件
            调用init_ext方法
            调用init_blue方法
        settings
            App运行的环境配置
            运行环境
        ext（扩展的，额外的）
            用来初始化第三方的各种插件
            Sqlalchemy对象初始化 数据库
            Session初始化
        views
            蓝图
            创建
            注册到app上
        models
        	定义模型
```

### 2.flask-migrate(模型迁移)

```
步骤:
	1.pip install flask-migrate
	2.ext:
		migrate = Migrate()
		migrate.init_app(app=app,db=db)
	3.主文件里:
		manager.add_command('DDBB',MigrateCommand)
	4.python manager.py DDBB init  第一次使用(生成文件夹)
	  python manager.py DDBB migrate  生成迁移文件
	  	不能生成有两种情况:(1)模型定义完成从未调用,（2）数据库已经有模型记录
	  python manager.py DDBB upgrade  	升级
	  python manager.py DDBB downgrade	降级
	5.创建用户文件
      python manager.py db migrate  --message ‘创建用户’
```

