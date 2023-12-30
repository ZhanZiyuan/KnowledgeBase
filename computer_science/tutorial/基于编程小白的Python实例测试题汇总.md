# 基于编程小白的Python实例测试题汇总

> Edited by *Ziyuan Zhan*
>> 来自[微信](https://mp.weixin.qq.com/s?__biz=MzIwNDA1OTM4NQ==&mid=2649543912&idx=2&sn=0fe7c701ba786570b49e5ba7d7d6fc7a&chksm=8edd937eb9aa1a68a0fe05760f9e3dfb663d6960e22bf4a240e350eb7e4b00b38b2efe805bac&mpshare=1&scene=23&srcid=&sharer_sharetime=1586505629631&sharer_shareid=4213a2a8cfd003cfb18b4baf78cb8f11#rd)

## 1. Python数字求和

```Python
#用户输入数字
num1=input('请输入第一个数：')
num2=input('请输入第二个数：')
#求和
sum=float(num1)+float(num2)
#要做运算，必须保证运算之前将字符格式转为整形init或浮点型float

#第一种显示方式：格式化输出
print('两个数字相加是结果是：%d'%sum)
#第二种显示方式：.format()
print('数字{0}和{1}相加结果为：{2}'.format(num1,num2,sum))
```

## 2. 平方根√￣，例：√￣16=4

```Python
num=float(input('请输入一个数字：'))
num_sqrt=num**0.5
print(' %0.3f 的平方根为 %0.3f'%(num,num_sqrt))#小数点后3位的浮点数
```

## 3. 计算三角形面积（海伦公式）

```Python
a=float(input('请输入三角形的第一边长：'))
b=float(input('请输入三角形的第二边长：'))
c=float(input('请输入三角形的第三边长：'))

#计算半周长
s=(a+b+c)/2

#计算面积
area=(s*(s-a)*(s-b)*(s-c))**0.5
print('三角形的面积是：%0.2f'%area)
```

## 4. 生成随机数

```Python
import random
print(random.randint(0,9))
```

## 5. 判断奇偶数

```Python
num=int(input('请输入一个数，判断奇偶数：'))
if num%2==0:
    print('%d是偶数'%num)
else:
    print('%d不是偶数'%num)
```

## 6. 判断闰年

（能被400整除 或 能被4整除而不能被100整除的年份）

```Python
num=int(input('请输入一个年份，判断是不是闰年：'))
if num%100==0:
    if num%400==0:
        print('%s年是闰年'%num)
    else:
        print('%s年不是闰年'%num)
else:
    if num%4==0:
        print('%s年是闰年'%num)
    else:
        print('%s年不是闰年'%num)
```

## 7. 判断是不是质数

```Python
num=int(input('请输入一个数，判断是不是质数：'))
if num>1:
    for i in range(2,num):
        if num%i==0:
            print('%s不是质数'%num)
            break
    else:
        print('%s是质数'%num)
else:
    print('请输入大于1的数')
```

## 8. 阶乘

```Python
num=int(input('请输入一个数，计算阶乘：'))

f=1
if num<0:
    print('负数没有阶乘')
if num==0:
    print('0的阶乘是1')
else:
    for i in range(1,num+1):
        f=f*i
print('%s的阶乘是%s'%(num,f))
```

## 9. 九九乘法表

```Python
for i in range(1,10):
    for j in range(1,i+1):
        print('%s*%s=%s'%(i,j,i*j),end=' ') #print()函数自带换行'\n'，这里去掉，让输出完这一段后再换行
    print() #print() == print('\n\t')
```

## 10. 判断是不是数字【这个得引入库】

(略)

## 11. Python 十进制转二进制（bin）、八进制（oct）、十六进制（hex）

```Python
dec=int(input('请输入数字：'))

print('十进制数为：',dec)
print('转换为二进制为：',bin(dec))
print('转换为十进制为：',oct(dec))
print('转换为十六进制为：',hex(dec))
```

## 12. 最大公约数

```Python
# 定义一个函数
def hcf(x,y):
    """该函数返回两个两个数的最大公约数"""

#获取最小值
    if x>y:
        smaller=y
    else:
        smaller=x

    for i in range(1,smaller+1):
        if ((x%i==0) and (y%i==0)):
            hcf=i

    return hcf

#用户输入两个数字
num1=int(input('请输入第一个数字：'))
num2=int(input('请输入第二个数字：'))

print(num1,'和',num2,'的最大公约数为',hcf(num1,num2))
```

## 13. 生成日历

```Python
#引入日历模块
import calendar

#输入指定年月
yy=int(input('请输入年份：'))
mm=int(input('请输入月份：'))

#显示日历
print(calendar.month(yy,mm)) #注意这里格式
```

## 14. 素数

>来自[CSDN](https://blog.csdn.net/Real_Tino/article/details/68947401)

```Python
n = int(input("please enter the number："))
for i in range(2, n):
    if n % i == 0:
        print(" %d is not a prime number！" % n)
        break
else:
    print(" %d is a prime number！" % n)
```

这里要细细品味这段代码，`else`其实不是和`if`是一对，而是和`for`并排的。
我们常见的是`if-else`或者`if-elif-else`诸如此类，但其实`for`也可以和`else`搭配出现。
在这段代码里，当某一次遍历结果余数为0后，`break`生效，那循环就结束了，那与之成对出现的`else`代码也就不执行了；
当所有遍历结束后没有一次余数为0，那该循环就转到`else`开始执行，打印输出“该数为质数”。
