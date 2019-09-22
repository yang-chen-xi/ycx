# 前言

**用Python代码（flask，django）链接数据库和页面**

**将数据库的数据通过Python代码在页面中显示出来**

**数据库和页面之间的数据的交互 ---》web后端开发**



web后端开发的三大语言：

+ JAVA：中大型企业级开发，多线程，开发周期长
+ PHP：小型企业级开发，单线程
+ PYTHON：开发周期短，多线程



# 笔记

1.创建flask项目

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello World!'

if __name__ == '__main__':
    app.run()
```

2.启动flask对接的服务器  开发者服务器

​	Python 文件的名字

​	例：python app.py

3.（1）在终端中写flask代码

   （2）专业版  create project  选择flask

   （3）社区版  可以直接创建文件，代码和终端写的一致

4.服务器默认的端口号是5000

5.修改端口号
```
（1）在run方法中修改 ：`host=字符串  port=字符串/整数`

（2）命令行参数：

		实现步骤：1.修改app.py 为 manager.py

				2.把app交给manager管理：  manager = Manager(app=app)

				3.app.run()修改为manager.run()	

		启动命令：Python  manager.py runserver  -h -p -r
```


6.属兔函数返回值

7.注意：如果我们修改的是python代码，服务器会自动重启；如果修改的是css，js，html，服务器不会自动重启，需要手动重启



WSGI：web服务器网关接口

# 学习课程

### 1. 框架简介

（1）基于Python的web（微）框架

```
重量级框架django（轻重量：框架的核心代码的多少）
	为了方便业务程序的开发，提供了丰富的工具及其组件
轻量级框架flask
	中提供web核心功能，自由灵活，高度定制，Flask也被称为“microframework”，因为它使用简单的核心，用
```

（2）官方文档

```
http://flask.pocoo.org/docs/0.12/      英文
http://docs.jinkan.org/docs/flask/     中文
```



（3）Flask 依赖库

```
jinja2			模板引擎
werkzeug WSGI	工具集
Itsdangerous	基于Django的签名模块
```

（4）Flask流行的主要原因

```
 1 有非常齐全的官方文档，上手非常方便
 2 有非常好的扩展机制和第三方扩展环境，工作中常见的软件都会有对应的扩展，动手实现扩展
 也很容易
 3 社区活跃度非常高    flask的热度已经超过django好几百了
 4 微型框架的形式给了开发者更大的选择空间
```



### 2.BS/CS

**概念：**

```
BS：B browser 浏览器 S server 服务器  主流
CS：C client 客户端  S Server 服务器
```

**CS/BS区别 ××××重点要背××××**

| 对象 | 硬件环境 | 客户端要求 | 安装 | 升级与维护 | 安全性 |
| ---- | -------- | ---------- | ---- | ---------- | ---------- |
| C/S | 用户固定,并且处于相同区域,要求拥有相同的操作系统. | 客户端的计算机电脑配置要求高 | 每一个客户端都必须安装和配置软件 | CS每一个客户端都要升级程序.可以采用自动升级 | 一般面向相对固定的用户群,程序更加注重流程,它可以对权限进行多层次校验,提供更安全的存取模式,对信息的控制能力很强,一般高度机密的信息系统CS结构适宜 |
| BS | 要有操作系统的浏览器,与操作系统平台无关 | 客户端的计算机电脑配置要求低 | 可以在任何地方进行操作而不用安装任何专门的软件. | 不必安装及维护 |  |



### 3.MVC/MTV

```
MVC：软件架构思想
	简介：
		MVC开始是存在于桌面程序中的，M是指业务模型 model，V是指用户界面 view，C则是控制器 controler，使用MVC的目的是将M和V的实现代码分离，从而使同一个程序可以使用不同的表现形式。比如一批统计数据可以分别用柱状图、饼图来表示。C存在的目的则是确保M和V的同步，一旦M改变，V应该同步更新.实现了模型层的复用
	核心思想:解耦合
	面向对象语言:高内聚,低耦合
	Model
		模型
		封装数据的交互操作
			CRUD
	View
		视图
		是用来将数据呈现给用户的
	Controller
		控制器
		接受用户输入输出
		用来协调Model和View的关系，并对数据进行操作，筛选
	流程
		控制器接受用户请求
		调用模型，获取数据
		控制器将数据展示到视图中
```

![img](https://gss3.bdstatic.com/-Po3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike80%2C5%2C5%2C80%2C26/sign=7948cf4dbf096b63951456026d5aec21/b03533fa828ba61edbddc04d4034970a304e59a4.jpg)



MTV也叫做MVT

```
MTV
	也叫做MVT
	本质上就是MVC，变种
	Model
		同MVC中Model
	Template
		模板
		只是一个html，充当的是MVC中View的角色，用来做数据展示
	Views
		视图函数
		相当于MVC中Controller
```

#### 4.Flask基本使用

(1）虚拟环境的创建

```
1.创建flask的虚拟环境
	mkvirtualenv Flaskpython1905 -p /usr/bin/python3
2.查看虚拟环境
	pip freeze
	pip list

3.虚拟环境迁移
	pip freeze > requirements.txt
		迁出
	pip install -r requirements.txt
		迁入
```

(2)Flask项目的创建

```
1.安装
	国外源  pip install flask
	国内源  pip install flask -i https://pypi.douban.com/simple
2.创建项目
	mkdir python1905 mkdir Flaskday01  mkdir FirstFlask  vim HelloFlask.py
	代码结构
		from flask import Flask
         app = Flask(__name__)

        @app.route("/")
        def index():
            return "Hello"
        app.run()
3.启动服务器  python  文件名字.py
	默认端口号  5000  只允许本机连接
```

3）启动服务器参数修改

```
run方法中添加参数
	在启动的时候可以添加参数  在run（）中
	debug
		是否开启调试模式，开启后修改过python代码自动重启
		如果修改的是html/js/css 那么不会自动重启
	host
		主机，默认是127.0.0.1 指定为0.0.0.0代表本机ip
	port
		指定服务器端口号
	threaded
		是否开启多线程
```

扩展：PIN码

```
全称Personal Identification Number.就是SIM卡的个人识别密码。手机的PIN码是保护SIM卡的一种安全措施，防止别人盗用SIM卡，如果启用了开机PIN码，那么每次开机后就要输入4到8位数PIN码。
在输入三次PIN码错误时，手机便会自动锁卡，并提示输入PUK码解锁，需要使用服务密码拨打运营商客服热线，客服会告知初始的PUK码，输入PUK码之后就会解锁PIN码。
```

（4）命令行参数

```
	1.安装
		pip install flask-script
		作用
			启动命令行参数
	2.初始化
		修改  文件.py为manager.py
		manager = Manager(app=app)
		修改 文件.run()为manager.run()
	3.运行
		python manager.py runserver -p xxx -h xxxx -d -r
          参数
          - p  端口 port
          - h  主机  host
          - d  调试模式  debug
          - r  重启（重新加载） reload（restart）
```

#### 5.视图函数返回值

```
	（1）index返回字符串
		@app.route('/index/')
         def index():
            return 'index'
	（2）模板first.html
		@app.route('/first/')
         def hello():
            return render_template("test.html")
      静态文件css
           注意
           <link rel="stylesheet" href="/static/css/hello.css">
```

#### 6.Flask基础结构

```
App
	templates
		模板
		默认也需要和项目保持一致
	static
		静态资源
		默认需要和我们的项目保持一致，在一个路径中，指的Flask对象创建的路径
	views
	models
	坑点
		执行过程中manager.py和其他的文件的路径问题
	第二个坑--封装__init__文件--
```

#### 7.蓝图

```Python
蓝图
	1. 宏伟蓝图（宏观规划）
	2. 蓝图也是一种规划，主要用来规划urls（路由）
	3. 蓝图基本使用
  	- 安装
     - pip install flask-blueprint
     - 初始化蓝图   blue = Blueprint('first',__name__)
     - 调用蓝图进行路由注册  app.register_blueprint(blueprint=blue)
     
# 坑: 蓝图对象的使用和创建都必须在views中
# 注册蓝图应该在manager里
```

#### 8.Flask请求流程

```python
# Flask的核心作用:路由的分发
# Tornado的核心作用:websocket
Flask请求流程
	请求到路由   app.route()
	视图函数   
	视图函数和models交互
	模型返回数据到视图函数
	视图函数渲染模板
	模板返回给用户
```

![img](https://upload-images.jianshu.io/upload_images/1801379-02bfe06281d809cf.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200)

#### 9.Flask路由参数

```python
# 路由参数额基本结构 /资源路径/<变量>/
# 路由参数的访问路径http://127.0.0.1:5000/testRoute/1/
# 路由参数的名字一定要和视图函数的参数一致
# 路由参数传递到视图函数中,是字符串类型 

# 路由参数的类型,默认为字符串
```

```python
带参数的请求
	从客户端或者浏览器发过来的请求带参数
	    @blue.route('/getstudents/<id>/')
        def getstudents(id):
           return '学生%s'+id
    路由参数
		基础语法
			<converter:var_name>
				书写的converter可以省略，默认类型就是string
		converter
			（1）string
                      接收的时候也是str， 匹配到 / 的时候是匹配结束
                      @blue.route('/getperson/<string:name>/')
                      def getperson(name):
                          print(name)
                          print(type(name))
                          return name
			（2）path
                      接收的时候也是str， / 只会当作字符串中的一个字符处理
                      @blue.route('/getperson1/<path:name>/')
                        def getperson1(name):
                            print(name)
                            print(type(name))
                            return name
# string和path的区别:
# string遇到/ 会当做介乎标签
#path 遇到 / 会当做一个字符串
    
			（3）int
                       @blue.route('/makemoney/<int:money>/')
                       def makemoney(money):
                            print(type(money))
                            return '1'
			（4）float
                        @blue.route('/makemoneyfloat/<float:money>/')
                        def makemoney(money):
                              print(type(money))
                              return '1'
			
			（5）uuid
                        uuid 类型，一种格式
                        @blue.route(('/getuu/'))
                        def getuu():
                              uu = uuid.uuid4()
                              print(uu)
                              return str(uu)

                        ------------------------------------
                        @blue.route('/getuuid/<uuid:uuid>/')
                        def getuuid(uuid):
                              print(uuid)
                              print(type(uuid))
                              return '2'
			（6）any
                        任意一个
                        已提供选项的任意一个 而不能写参数外的内容  注意的是/
                        @blue.route('/getany/<any(a,b):p>/')
                        def getany(p):
                            return '1'
```



#### 请求方式

请求方式又叫http方法

五种请求方式:

get(获取)	post(添加)	delete(删除)	put(修改全部属性)		patch(修改的是部分户型)



+ 需求:执行一个视图函数,然后跳转到一个模板 login.html

  在模板中输入用户名字.然后点击登录

  点击之后,显示欢迎光临红浪漫

```python
# 路由默认只支持get  head option 请求方式,不支持post  delete

# 如果想让路由支持post delete put patch方法,可以在route方法中添加一个参数,这个参数是methods=[]

#methods列表的元素的大小写都可以

@blue.route('/login/',methods=['post','delete'])
def login():
    return '欢迎光临红浪漫'

# 状态码
#200 成功
#301 重定向
#302 永久重定向
#403 forbidden 防跨站攻击
#404 路径错误
#405 请求方式错误
#500 服务器  业务逻辑错误

```



#### 10.postman

```
请求方式
	postman
		模拟请求工具
			方法参数中添加methods=['GET','POST']
	安装
		https://blog.csdn.net/Shyllin/article/details/80257755
	1. 默认支持GET，HEAD，OPTIONS
	2. 如果想支持某一请求方式，需要自己手动指定
	3. 在route方法中，使用methods=["GET","POST","PUT","DELETE"]
```

#### 11.反向解析

```python
@blue.route('/testReverse1/')
def testReverse1():
    #反向解析的语法:url_for(蓝图的名字.方法的名字)
    #反向解析获取的是请求资源李静
    # 获取testReverse的请求资源路径
    s = url_for('blue.testReverse')
    print(s)
    s1 = url_for('blue.testPstman')
    print(s1)
    # 应用场景:
    #  (1) redirect('/index/')从定向到index请求.尽量不要使用硬编码
    #  (2)页面中,不要使用用编码  form action='/login/'
    	form action = url_for('blue.login')
```



```
反向解析
	（1）概念：
		获取请求资源路径
	（2）语法格式：
		url_for(蓝图的名字.方法名字)
	（3）使用：
         @blue.route("/heheheheheheheheheehhehe/", methods=["GET","POST","PUT"])
          def hehe():
              return "呵呵哒"


          @blue.route("/gethehe/")
          def get_hehe():
              p = url_for("first.hehe")
          return p

```

