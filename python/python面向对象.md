pyinstaller -F -w ftest.py 

**python对象类型**

- 数字 				1234, 3.1415, 3+4j,Decímal, Fraction

- 字符串 				'spam', "guído's",b'a\×o1c‘

- 列表 				[1,[2,‘thiee'],4]

- 字典 				{'foud':'5pam','taste':'yum'}

- 元组 				(1,'spam',4,'U‘)

- 文件 				myﬁle=open( 'eggs' , 'r')

- 集合 				set('abc'), {'a', 'b', 'c‘}

- 其他类型 			类型_ None、 布尔型

- 编程单元类型 		函数、 模块、 类 (参见第四部分、 第五部分和笫六部分)

- 与实现相关的类型 	编译的代码堆栈踉踪 (参见笫四部分和第七部分)


python对象
​	**不可变性 :** 数字 字符串 和 元组
​	**可变性 :** 列表 字典



####  面向对象

- 类(Class): 用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。 
- 类变量：类变量在整个实例化的对象中是公用的。类变量定义在类中且在函数体之外。类变量通常不作为实例变量使用。 
- 数据成员：类变量或者实例变量, 用于处理类及其实例对象的相关的数据。 方法重写：如果从父类继承的方法不能满足子类的需求，可以对其进行改写，这个过程叫方法的覆盖（override），也称为方法的重写。
-  局部变量：定义在方法中的变量，只作用于当前实例的类。 
- 实例变量：在类的声明中，属性是用变量来表示的。这种变量就称为实例变量，是在类声明的内部但是在类的其他成员方法之外声明的。 
- 继承：即一个派生类（derived class）继承基类（base class）的字段和方法。继承也允许把一个派生类的对象作为一个基类对象对待。例如，有这样一个设计：一个Dog类型的对象派生自Animal类，这是模拟"是一个（is-a）"关系（例图，Dog是一个Animal）。 
- 实例化：创建一个类的实例，类的具体对象。 方法：类中定义的函数。 
- 对象：通过类定义的数据结构实例。对象包括两个数据成员（类变量和实例变量）和方法



```python
class Employee:
   '所有员工的基类'
   empCount = 0
 
   def __init__(self, name, salary):  # [2]
      self.name = name
      self.salary = salary
      Employee.empCount += 1     # [1]
   
   def displayCount(self):
     print "Total Employee %d" % Employee.empCount
```

​	[1]  empCount 变量是一个类变量，它的值将在这个类的  ***所有实例***  之间共享,可以在内部类或外部类使用 Employee.empCount 访问。

​	[2] 第一种方法__init__()方法是一种特殊的方法，被称为类的**构造函数**或初始化方法，当**创建了这个类的实例时就会调用**该方法



**self代表类的实例 , 而非类**

​	类的方法与普通的函数只有一个特别的区别——它们必须有一个额外的**第一个参数名称**, 按照惯例它的名称是 self,  self 不是 python 关键字,可以使用其他名称

```python
class Test:
    def prt(self):
        print(self)				 # <__main__.Test object at 0x00000000028BB588>
        print(self.__class__)    # <class '__main__.Test'>   # 指向类
 
t = Test()
t.prt()
```



析构函数  del , 在对象销毁的时候被调用

```python
class Point:
   def __init__( self, x=0, y=0):
      self.x = x
      self.y = y
   def __del__(self):                     # 析构函数
      class_name = self.__class__.__name__
      print class_name, "销毁"
 
pt1 = Point()
pt2 = pt1
pt3 = pt1
print id(pt1), id(pt2), id(pt3) # 打印对象的id   多次引用计数
del pt1
del pt2
del pt3

'''
3083401324 3083401324 3083401324
Point 销毁
'''
```

##### 



##### 类的继承	[^2]

- ​	子类不重写 ____init____，实例化子类时，会自动调用父类定义的 ____init____。


- ​	如果重写了____init____ 时，实例化子类，就不会调用父类已经定义的 ____init____，​	[^1]


- ​	如果重写了__init__ 时，要继承父类的构造方法，可以使用 super 关键字：


```python
' super(子类，self).__init__(参数1，参数2，....) '

class Father(object):
    def __init__(self, name):
        self.name=name
        print ( "name: %s" %( self.name))
    def getName(self):
        return 'Father ' + self.name
 
class Son(Father):
    def __init__(self, name):
        super(Son, self).__init__(name)
        print ("hi")
        self.name =  name
    def getName(self):
        return 'Son '+self.name
 
if __name__=='__main__':
    son=Son('runoob')
    print ( son.getName() )   
    
'''  父类构造 子类构造 都调用
name: runoob
hi
Son runoob
'''
```

[^1]: Python 子类继承父类构造函数说明 http://www.runoob.com/w3cnote/python-extends-init.html

[^2]: python类的继承,类的私有属性 http://www.runoob.com/python/python-object.html