## 学习目标

+ request
+ response



## 学习课程

### 1.request

```python
@blue.route('/testRoute/')
def testRoute():
    # mysql 3306 ; mongodb 27017 ; oracle 1521; redis 6379 
    #http 80 ; https 443 ;
    #ftp 21 ; ssh 22
    
    # 获取的是请求方式/http方法
    print(request.method)
    
    # 去掉请求参数的路径
    print(request.base_url)
    
    # 主机的路径不带请求资源路径
    print(request.host_url)
    
    #完整的url路径(请求资源路径,请求参数)
    print(request.url)
    
    #主机地址; 应用场景:反爬虫
    print(request.remote_addr)
    
    #应用场景:文件上传
    print(request.files)
    
    #请求头
    print(request.headers)
    
    # 请求资源路径  应用场景:购物车
    print(request.path)
    
    #获取请求额cookies
    print(request.cookies)
    
    print()
    
    return 'testRequest'
```



+ request是一个内置对象;内置对象不需要创建就可以直接使用



### 2.response 视图函数的返回值

+ 字符串
+ render_template
+ make_response
+ redirect
+ Response

```python
# 视图函数返回字符串
@blue.route('/testResponse/')
def testResponse():
    return '床前明月光'

# 视图函数返回一个模板
@blue.route('/testResponse2/')
def tsetResponse2():
    s = render_template('testResponse2.html')
    return s

# 视图函数返回一个make_response()  返回response类型
@blue.route('/testResponse3/')
def testResponse3():
    r = make_response('<h1>举头望明月</h1>')
    return r

# 视图函数返回redirect
@blue.route('/index/')
def index():
    return '好客山东欢迎您'
@blu.route('/testResponse4/')
def testResponse4():
    # r = redirect('/index/')
    r = redirect(url_for('blue.index'))
    return r

# 视图函数返回Response对象
@blue.route('/testResponse5/')
def testResponse5():
    r = Response('低头思故乡')
    return r
```

总结:视图函数的返回值有2大类:

1. 字符串
   1. 普通字符串
   2. render_template
2. response
   1. make_response
   2. redirect
   3. Response



### 3. 异常

```Python
# 异常
@blue.route('/testAbort/')
def testAbort():
    abort(404)
    
    return 'testAbort'

#errorhandler抓取Flask中所有异常状态码,抓到抛出相同的状态码,就会执行下列方法
@blue.errohandler(404)
def testAbort1(Exception):
    return '找不到页面啦'
```



### 4.会话技术

#### (1) cookie

***设置cookie必须要有response对象***

```
Cookie
	1.客户端会话技术
	2.所有数据存储在客户端
	3.以key-value进行数据存储层
	4.服务器不做任何存储
	5.特性
		(1)支持过期时间
			max_age  毫秒
			expries  具体日期
		(2)根据域名进行cookie存储
		(3)不能跨网站（域名）
		(4)不能跨浏览器
		(5)自动携带本网站的所有cookie
	6.cookie是服务器操作客户端的数据
	7.通过Response进行操作
```



cookie的使用

```python
#设置cookie :
	response.set_cookie('username',username)
#获取cookie
	username = request.cookie.get('username',游客)
#删除cookie
	response.delete_cookie('username')
```



需求:执行一个视图函数tologincookie,跳转到一个页面logincookie.html,输入一个用户名字,点击提交,跳转到welcomecookie.html,该页面的内容是:''欢迎xxx光临红浪漫''.如果没有经过登陆,直接跳转到welcomcookie.html,会显示'欢迎游客光临',如果已经登录然后跳转到welcomecookie.html,那么在欢迎xxx下面还有一个退出,然后退出,跳转到welcomcookie.html页面,显示'欢迎游客'



##### (2)session

```python
Session
	1.服务端会话技术
	2.所有数据存储在服务器中
	3.默认存在服务器的内存中
		- django默认做了数据持久化（存在了数据库中）
	4.存储结构也是key-value形势，键值对
	#【注】单纯的使用session是会报错的，需要使用在__init__方法中配置app.config['SECRET_KEY']=‘110’
```

**session的登录使用**

```python
#设置:
	session['username'] = username
# 获取
	sessionn.get('username')
# 删除
	resp.delete_cookie('session')
	session.pop('username')
```

##### (3)cookie和session总结

```
（1）cookie: 客户端浏览器的缓存；session: 服务端服务器的缓存
（2）cookie不是很安全，别人可以分析存放在本地的cookie并进行cookie欺骗，考虑到安全应当使用session
（3）session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能，考虑到减轻服务器性能方面，应当使用cookie
可以考虑将登陆信息等重要信息存放为session，其他信息如果需要保留，可以放在cookie中
```

##### (4)session持久化问题

- 持久化简介

  ```
  1.django中对session做了持久化，存储在数据库中
  2.flask中没有对默认session进行任何处理
      - flask-session 可以实现session的数据持久化
      - 可以持久化到各种位置，更推荐使用redis
          - 缓存在磁盘上的时候，管理磁盘文件使用lru, 最近最少使用原则
  ```

- 持久化实现方案

```python
1.pip install flask-session
			在国内源安装
			pip install flask-sessin -i https://pipy.douban.com/simple
2.初始化Session对象 
	（1）持久化的位置
		配置init中app.config['SESSION_TYPE'] = 'redis'
		
	（2）初始化
		创建session的对象有2中方式 分别是以下两种
        # 在init中
		1 Session(app=app)
		2 se = Session()   se.init_app(app = app)
	# 如果报错为 NO medol named redis,证明虚拟环境中没有redis模块				
	（3）安装redis   
		pip install redis
				
	 (4)需要配置SECRET_KEY='110'
		 注意：flask把session的key存储在客户端的cookie中，通过这个key可以从flask的内存中获取用户的session信息，出于安全性考虑，使用secret_key进行加密处理。所以需要先设置secret_key的值。
			 	
	（5）其他配置--视情况而定
    # 定义session前缀
		app.config['SESSION_KEY_PREFIX']='flask'
    # 如果设置为True，则关闭浏览器session就失效。
    	app.config['SESSION_PARMANENT'] = Flask
		
   特殊说明：
        查看redis内容
              redis-cli
              keys *
              get key
        session生存时间31天	
            ttl session
           flask的session的生存时间是31天，django的session生存时间是15天
```



### 5.Template 模板

+ 模板语法

  1.基本语法

  ```
  模板语言动态生成的html
  		{{ var }}  变量的接收
  			从views传递过来的数据
  			前面定义出来的数据
  ```

  2.结构标签

  ```Python
  （1）block
          首次出现挖坑操作
          第二次出现填坑操作
          #第N次出现，填坑操作，会覆盖前面填的坑
          #不想被覆盖，需要添加 {{ super() }}
  （2）extends
  	    继承
  （3）include
  		包含，将一个指定的模板包含进来
  ```

  3.宏定义（macro）

  ```html
  （1）无参
  	{% macro say()%}
      	你饿了吗？？？
  	{% endmacro %}
  		
  （2）有参
  	{% macro createUser(name,age)%}
     		欢迎{{ name }} 心理没点数吗 你都{{ age }}大了
  	{% endmacro %}
  		
  （3）外文件中的宏定义调用需要导入也可以include
  	{% macro getUser(name)%}
      	欢迎光临红浪漫{{ name }},拖鞋手牌拿好,楼上2楼左转,男宾一位
  	{% endmacro %}
  		
  	{% from ‘html文件’ import yyy %}
  	{{ getUser('action') }}
  ```

  4.for循环

  ````html
  {% for i in [view传过来的列表] %}
  	<li> {{ i }} </li>
  {% endfor %}
  
  {% for i in score %}
          {% if loop.first %}
              <li style="color: green">{{ i }}</li>
          {% elif loop.last %}
              <li style="color: blue">{{ i }}</li>
          {% else %}
              <li style="color: pink">{{ i }}</li>  
          {% endif %}
      {% endfor %}
  ````

  5.过滤器

  ```html
  语法格式：{{ [传过来的value]|xxx|yyy|zzz }}
  没有数量限制
  	lower
  	upper
  	trim		去空格
  	reverse		反转
  	striptags   渲染之前将值中的标签去掉
  	safe        标签生效
  	eg:
  		{% for c in config %}
              <li>{{ loop.index0 }}:{{ loop.index}}:{{ c|lower|reverse }}</li>
      	{% endfor %}
  ```



### 6.models (通过模型操作表)

+ 原生SQL缺点:
     （1）代码利用率低，条件复杂代码语句越过长，有很多相似语句
     （2）一些SQL是在业务逻辑中拼出来的，修改需要了解业务逻辑

+ 优点

  （1）易用性，可以有效减少重复SQL
  （2）性能损耗少
  （3）设计灵活，可以轻松实现复杂查询
  （4）移植性好

+ SQLalchemy

  ```python
  flask-sqlalchemy
  	使用步骤:
  	1.pip install flask-sqlalchemy
  	2.创建SQLALCHEMY对象
  		①：db=SQLAlchemy(app=app)
  		②：db=SQLAlchemy()
  		上面这句话一般会放到models中因为需要db来调用属性db.init_app(app=app)
  			(在init中调用)
  	3.config中配置" app.config['SQLALCHEMY_DATABASE_URI'] =  "
  		数据库 + 驱动 :// 用户:密码@ 主机:端口/数据库
  		dialect+driver://username:password@host:port/database
  		eg:mysql+pymysql://root:1234@localhost:3306/flask1905
  	4.执行:views中db.create_all()
  		注意：有坑
  		（1）primary-key:添加主键
  		（2）SQLALCHEMY_TRAKE_MODIFICATIONS:
  		  在init中添加:app.config[‘SQLALCHEMY_TRAKE_MODIFICATIONS’]=False
  ```

  ```python
  使用:()
  1）定义模型
  	继承Sqlalchemy对象中的model
  	eg:
  		'db = SQLAlchemy()' 注意括号
                  
  		class User(db.Model):
          id = db.Column(db.Integer,primary_key=True,autoincrement=True)l
          name = db.Column(db.String(32))
          age = db.Column(db.Integer)
  (2)创建
  	db.create_all()
  (3)删除
  	db.drop_all()
  (4)修改表名
  	__tablename__ = "Worker"
  (5)数据操作
  	添加
      	db.session.add(对象)
      	db.session.commit()
      查询
      	模型.query.all()
  ```

  

