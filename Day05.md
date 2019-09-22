### 逻辑运算

```python
@blue.route('/getLogic/')
def getLogic():
    # 与
    song = Song.query.filter(an_(Song.id==1,Song.name=='[名字]'))[0] #baseQuery对象,要拿出一个数据
    
    # 或
    song = Song.query.filter(or_(Song.id==1,Song.name=='[名字]'))[0]
    
    # 非,条件只能有一个,导包注意是sqlalchemy的包
    songs = Song.query.filter(not_(Song.id==1,Song.name=='[名字]'))
    for song in songs:
    	print(song.id,song.name)
        
    # in
    songs = Song.query.filter(Song.id.in_([1,2,3,4]))
    for song in songs:
        print(song.id,song.name)
```

### 数据定义

```
(1)字段定义
	Integer
	String
	Date
	Boolean
(2)约束
	primary_key 
	autoincrement
	unique
	defaul
	index
	
```

### 模型关系

##### 1.一对多

```
1.relationship函数
	sqlalchemy对关系之间提供的一种便利的调用方式,关联不同的表
2.backref
	对关系提供反向引用的生命,在Parent类上声明心属性的简单方法,只有可以在Child.person来获取这个对象的person
```

(1)=user = User.query.get(id=3)

print(user.name)

默认情况下调用get方法的时候就发送的sql语句,如果我们使用到了dynamic就代表的是懒加载或者叫延迟加载,不使用对象的属性或防发的时候就不发送SQL语句

(2) user = User.query.all()

​	for user in users:

​	print(user.name)

默认情况下调用get方法的时候就发送的sql语句,如果使用dynamic,那么就可以在便利的死后发送sql语句

```python
@blue.rout('/addParent/')
def addParent():
    parent = Parent()
    parent.name = 'zhangsan'
    
    child1 = Child()
    child1.name = 'zhangsan'
    
    child2 = Child()
    child2.name = 'zhangwu'
    
    child_list = [child1,child2]
    parent.children = child_list
    
    db.session.add(parent)
    db.session.commit()
    
    return '添加成功'
```

```python
# 从差主  给一个child,查询parent
@blue.route('/getParent/')
def getParent():
    parent = Parent.query.filter(Child.id == 1) [0]
    print(parent)
```



### 分页器

