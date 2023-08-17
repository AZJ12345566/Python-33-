# Python-33-
Python学习笔记(33)
# p118 特殊方法
a=20
b=100
c=a+b  #两个整数类型的对象的相加操作
c=a.__add__(b)
print(c)
print(d)

class Student:
    def __unit__(self,name):
        self.name=name
    def __add__(self,other):
        return self.name+other.name
    def __len__(self):
        return len(self.name)

stu1=Student('张三')
stu2=Student('李四')

s=stu1+stu2
print(s)  #报错
#通过添加特殊方法__add__()可以正常输出
print(s)

lst=[11,22,33,44]
print(len(lst))  #这是一个内置函数计算len的长度
print(lst.__len__())  #与上一行代码输出值一样

print(len(stu1))  #想实现对象的len必须现在类中定义这个用法



# p119 __new__与__init__演示创建对象的过程
class Person(object):
    
    def __new__(cls,*args,**kwargs):
        print('__new__被调用执行了，cls的调用值为{0}'.format(id(cls)))
        obj=super().__new__(cls)
        print('创建的对象的id为:{0}'.format(id(obj)))
        return obj
        
        def __init__(self,name,age):
        print('__init__被调用执行了,self的id值为:{0}'.format(id(self)))
        self.name=name
        self.age=age

print('object这个类对象的id为:{0}'.format(id(object)))
print('Person这个类对象的id为:{0}'.format(id(Person)))

#创建Person类的实例对象
p=Person('张三'，20)
print('p1这个Person类的实例对象的id:{0}'.format(id(p1)))



# p120 类的赋值与浅拷贝
class CPU:
    pass
class Disk:
    pass
class Computer:
    def __init__(self,cpu,disk):
        self.cpu=cpu
        self.disk=disk

#(1)变量的赋值
cpu1=CPU()
cpu2=cpu1
print(cpu1,id(cpu1))
print(cpu2,id(cpu2))

#(2)类的浅拷贝
disk=Disk()  #创建一个硬盘类的对象
computer=Computer(cpu1,disk)  #创建一个计算机类的对象


#浅拷贝
import copy
print(disk)
computer2=copy.copy(computer)
print(computer,computer.cpu,computer.disk)
print(computer2,computer2.cpu,computer2.disk)

#浅拷贝大概意思就是：对象包含的字对象内容不拷贝，因此，原对象与拷贝对象会引用同一个子对象
#这里的computer会拷贝两个id是一样的，而子对象是不拷贝的，因此computer2指向的字对象也是和computer是相同的



# p121 深拷贝
computer3=copy.deepcopy(computer)
print(computer,computer.cpu,computer.disk)
print(computer3,computer3.cpu,computer3.disk)
#不仅把computer拷贝了，还把子对象拷贝了



# p122 什么叫模版_模块化编程的好处
def fun():
    pass
def fun2():
    pass

class Student:
    native_place='吉林'  #类属性
    def eat(self):
        self.name=name
        self.age=age
    @classmethod
    def cm(cls):
        pass
    @staticmethod
    def sm():
        pass

a=10
b=20
print(a+b)

#一个模块可以包含n多个函数，还可以包含n多个类，以及n多个语句



# p123 模块的导入
import math  #关于数值运算的模块
print(id(math))
print(type(math))
print(math)
print(math.pi)
print(dir(math))
print(math.pow(2,3),type(math.pow(2,3)))  #这里的pow计算的是2的3次方
print(math.ceil(9.001))  #输出10
print(math.floor(9.9999))  #输出为9

#第一种导入方法是import，第二种导入方法是from模块名称import函数/变量/类
from math import pi
print(pi)
print(pow(2,3))  #这个pow就不可以实现了，因为上面的导入方法只导入了math中的pi，如果要使用就必须在导入一遍
print(math.pow(2,3))

def add(a,b):
    return a+b
def div(a,b):
    return a/b

#如何去导入自定义模块
import calc  #这里程序会报错，我们在文件栏单击右键点击选项Make Directory as -> Sources Root
print(calc.add(10,20))
print(calc.div(10,4))

from calc import add
print(add(10,20))
