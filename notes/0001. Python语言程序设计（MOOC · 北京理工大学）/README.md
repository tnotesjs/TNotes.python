# [0001. Python语言程序设计（MOOC · 北京理工大学）](https://github.com/tnotesjs/TNotes.python/tree/main/notes/0001.%20Python%E8%AF%AD%E8%A8%80%E7%A8%8B%E5%BA%8F%E8%AE%BE%E8%AE%A1%EF%BC%88MOOC%20%C2%B7%20%E5%8C%97%E4%BA%AC%E7%90%86%E5%B7%A5%E5%A4%A7%E5%AD%A6%EF%BC%89)

<!-- region:toc -->

::: details 📚 相关资源

- [📂 TNotes.yuque（笔记附件资源）](https://www.yuque.com/tdahuyou/tnotes.yuque/)
  - [TNotes.yuque.python.0001](https://www.yuque.com/tdahuyou/tnotes.yuque/python.0001)

:::

- [1. 本节内容](#1-本节内容)
- [2. 教程实验示例汇总](#2-教程实验示例汇总)
  - [2.1. 温度转换](#21-温度转换)
  - [2.2. python 蟒蛇绘制](#22-python-蟒蛇绘制)
  - [2.3. 天天向上的力量](#23-天天向上的力量)
  - [2.4. 文本进度条](#24-文本进度条)
  - [2.5. 身体质量指数](#25-身体质量指数)
  - [2.6. 圆周率的计算](#26-圆周率的计算)
  - [2.7. 七段数码管绘制](#27-七段数码管绘制)
  - [2.8. 科赫雪花小包裹](#28-科赫雪花小包裹)
  - [2.9. 基本统计值计算](#29-基本统计值计算)
  - [2.10. 文本词频统计](#210-文本词频统计)
  - [2.11. 自动轨迹绘制](#211-自动轨迹绘制)
  - [2.12. 政府工作报告词云](#212-政府工作报告词云)
  - [2.13. 体育竞技分析](#213-体育竞技分析)
  - [2.14. 第三方库安装脚本](#214-第三方库安装脚本)
  - [2.15. 霍兰德人格分析雷达图](#215-霍兰德人格分析雷达图)
  - [2.16. 玫瑰花绘制](#216-玫瑰花绘制)
- [3. 常见问题](#3-常见问题)
  - [3.1. Python 语言、C 语言、Java 语言、VB 语言…… 到底哪种适合作为入门编程语言呢？](#31-python-语言c-语言java-语言vb-语言-到底哪种适合作为入门编程语言呢)
  - [3.2. Python 2.x 和 Python 3.x，该学习哪个版本？](#32-python-2x-和-python-3x该学习哪个版本)
  - [3.3. Python 语言是跨平台的吗？](#33-python-语言是跨平台的吗)
  - [3.4. Python 语言是面向对象语言吗？](#34-python-语言是面向对象语言吗)
  - [3.5. 在线开放课程只能看到视频，有问题谁来解答？](#35-在线开放课程只能看到视频有问题谁来解答)
  - [3.6. 这个课程需要配套教材或工具书吗？](#36-这个课程需要配套教材或工具书吗)
  - [3.7. 全国计算机等级考试二级 Python 科目有什么用？需要参加吗？](#37-全国计算机等级考试二级-python-科目有什么用需要参加吗)
  - [3.8. 这门 Python 语言课程来源于哪里？质量如何呢？](#38-这门-python-语言课程来源于哪里质量如何呢)
  - [3.9. 为什么开课团队这么执着于 Python 课程大纲及所谓的 “课程大纲版本”？](#39-为什么开课团队这么执着于-python-课程大纲及所谓的-课程大纲版本)
- [4. 引用](#4-引用)

<!-- endregion:toc -->

## 1. 本节内容

这一节记录的内容是“Python 语言程序设计（MOOC · 北京理工大学）”教程的一些学习笔记。

教程来源说明：这是 23.07 月份在 MOOC 上找的北理工的 Python 入门教程。

- 来源平台：[中国大学MOOC][1]
- 课程：[北京理工大学 - Python语言程序设计][2]

教程资料说明：

- 这篇笔记记录了实验示例代码，用于快速回顾这份教程讲解的相关知识点。
- 课件、视频、实验示例代码和相关素材资源等，可在 [TNotes.yuque][5] 中自行下载。

笔记阅读建议：

- 回顾时，重点看一开始的源码模块，确保每一节的程序示例都能够理解即可。
- 每一节笔记中都有对应的视频，如果遇到不理解的点，直接回看视频即可。

## 2. 教程实验示例汇总

### 2.1. 温度转换

::: code-group

```py [TempConvert.py]
# TempConvert.py
TempStr = input("请输入带有符号的温度值: ")
if TempStr[-1] in ["F", "f"]:
    C = (eval(TempStr[0:-1]) - 32) / 1.8
    print("转换后的温度是{:.2f}C".format(C))
elif TempStr[-1] in ["C", "c"]:
    F = 1.8 * eval(TempStr[0:-1]) + 32
    print("转换后的温度是{:.2f}F".format(F))
else:
    print("输入格式错误")

# 输出：
"""
请输入带有符号的温度值: 39C
转换后的温度是102.20F
"""
```

:::

### 2.2. python 蟒蛇绘制

::: code-group

```py [PythonDraw.py]
# PythonDraw.py
import turtle

turtle.setup(650, 350, 200, 200)
turtle.penup()
turtle.fd(-250)
turtle.pendown()
turtle.pensize(25)
turtle.pencolor("purple")
turtle.seth(-40)
for i in range(4):
    turtle.circle(40, 80)
    turtle.circle(-40, 80)
turtle.circle(40, 80 / 2)
turtle.fd(40)
turtle.circle(16, 180)
turtle.fd(40 * 2 / 3)
turtle.done()
```

:::

### 2.3. 天天向上的力量

::: code-group

```py [DayDayUpQ1.py]
# DayDayUpQ1.py
dayup = pow(1.001, 365)
daydown = pow(0.999, 365)
print("向上：{:.2f}，向下：{:.2f}".format(dayup, daydown))
# 向上：1.44，向下：0.69
```

```py [DayDayUpQ2.py]
# DayDayUpQ2.py
dayfactor = 0.019
dayup = pow(1 + dayfactor, 365)
daydown = pow(1 - dayfactor, 365)
print("向上：{:.2f}，向下：{:.2f}".format(dayup, daydown))
# 向上：962.89，向下：0.00
```

```py [DayDayUpQ3.py]
# DayDayUpQ3.py
dayup = 1.0
dayfactor = 0.01
for i in range(365):
    if i % 7 in [6, 0]:
        dayup = dayup * (1 - dayfactor)
    else:
        dayup = dayup * (1 + dayfactor)
print("工作日的力量：{:.2f} ".format(dayup))
# 工作日的力量：4.63
```

```py [DayDayUpQ4.py]
# DayDayUpQ4.py
def dayUP(df):
    dayup = 1
    for i in range(365):
        if i % 7 in [6, 0]:
            dayup = dayup * (1 - 0.01)
        else:
            dayup = dayup * (1 + df)
    return dayup


dayfactor = 0.01
while dayUP(dayfactor) < 37.78:
    dayfactor += 0.001
print("工作日的努力参数是：{:.3f} ".format(dayfactor))
# 工作日的努力参数是：0.019
```

:::

### 2.4. 文本进度条

::: code-group

```py [TextProBarV1.py]
# TextProBarV1.py
import time

scale = 10
print("------执行开始------")
for i in range(scale + 1):
    a = "*" * i
    b = "." * (scale - i)
    c = (i / scale) * 100
    print("{:^3.0f}%[{}->{}]".format(c, a, b))
    time.sleep(0.1)
print("------执行结束------")

"""
------执行开始------
 0 %[->..........]
10 %[*->.........]
20 %[**->........]
30 %[***->.......]
40 %[****->......]
50 %[*****->.....]
60 %[******->....]
70 %[*******->...]
80 %[********->..]
90 %[*********->.]
100%[**********->]
------执行结束------
"""
```

```py [TextProBarV2.py]
# TextProBarV2.py
import time

for i in range(101):
    print("\r{:3}%".format(i), end="")
    time.sleep(0.1)

# 100%
```

```py [TextProBarV3.py]
# TextProBarV3.py
import time

scale = 50
print("执行开始".center(scale // 2, "-"))
start = time.perf_counter()
for i in range(scale + 1):
    a = "*" * i
    b = "." * (scale - i)
    c = (i / scale) * 100
    dur = time.perf_counter() - start
    print("\r{:^3.0f}%[{}->{}]{:.2f}s".format(c, a, b, dur), end="")
    time.sleep(0.1)
print("\n" + "执行结束".center(scale // 2, "-"))

"""
-----------执行开始----------
100%[**************************************************->]5.22s
-----------执行结束----------
"""
```

:::

### 2.5. 身体质量指数

::: code-group

```py [CalBMIv1.py]
# CalBMIv1.py
height, weight = eval(input("请输入身高(米)和体重(公斤)[逗号隔开]: "))
bmi = weight / pow(height, 2)
print("BMI 数值为：{:.2f}".format(bmi))
who = ""
if bmi < 18.5:
    who = "偏瘦"
elif 18.5 <= bmi < 25:
    who = "正常"
elif 25 <= bmi < 30:
    who = "偏胖"
else:
    who = "肥胖"
print("BMI 指标为:国际'{0}'".format(who))

"""
请输入身高(米)和体重(公斤)[逗号隔开]: 1.66,66
BMI 数值为：23.95
BMI 指标为:国际'正常'
"""
```

```py [CalBMIv2.py]
# CalBMIv2.py
height, weight = eval(input("请输入身高(米)和体重(公斤)[逗号隔开]: "))
bmi = weight / pow(height, 2)
print("BMI 数值为：{:.2f}".format(bmi))
nat = ""
if bmi < 18.5:
    nat = "偏瘦"
elif 18.5 <= bmi < 24:
    nat = "正常"
elif 24 <= bmi < 28:
    nat = "偏胖"
else:
    nat = "肥胖"
print("BMI 指标为:国内'{0}'".format(nat))

"""
请输入身高(米)和体重(公斤)[逗号隔开]: 1.66,66
BMI 数值为：23.95
BMI 指标为:国内'正常'
"""
```

```py [CalBMIv3.py]
# CalBMIv3.py
height, weight = eval(input("请输入身高(米)和体重(公斤)[逗号隔开]: "))
bmi = weight / pow(height, 2)
print("BMI 数值为：{:.2f}".format(bmi))
who, nat = "", ""
if bmi < 18.5:
    who, nat = "偏瘦", "偏瘦"
elif 18.5 <= bmi < 24:
    who, nat = "正常", "正常"
elif 24 <= bmi < 25:
    who, nat = "正常", "偏胖"
elif 25 <= bmi < 28:
    who, nat = "偏胖", "偏胖"
elif 28 <= bmi < 30:
    who, nat = "偏胖", "肥胖"
else:
    who, nat = "肥胖", "肥胖"
print("BMI 指标为:国际'{0}', 国内'{1}'".format(who, nat))

"""
请输入身高(米)和体重(公斤)[逗号隔开]: 1.66,66
BMI 数值为：23.95
BMI 指标为:国际'正常', 国内'正常'
"""
```

:::

### 2.6. 圆周率的计算

::: code-group

```py [CalPiV1.py]
# CalPiV1.py
pi = 0
N = 100
for k in range(N):
    pi += (
        1
        / pow(16, k)
        * (4 / (8 * k + 1) - 2 / (8 * k + 4) - 1 / (8 * k + 5) - 1 / (8 * k + 6))
    )
print("圆周率值是: {}".format(pi))
# 圆周率值是: 3.141592653589793
```

```py [CalPiV2.py]
# CalPiV2.py
from random import random
from time import perf_counter

DARTS = 1000 * 1000
hits = 0.0
start = perf_counter()
for i in range(1, DARTS + 1):
    x, y = random(), random()
    dist = pow(x**2 + y**2, 0.5)
    if dist <= 1.0:
        hits = hits + 1
pi = 4 * (hits / DARTS)
print("圆周率值是: {}".format(pi))
print("运行时间是: {:.5f}s".format(perf_counter() - start))

"""
圆周率值是: 3.141568
运行时间是: 0.25680s
"""
```

:::

### 2.7. 七段数码管绘制

::: code-group

```py [SevenDigitsDrawV1.py]
# SevenDigitsDrawV1.py
import turtle


def drawLine(draw):  # 绘制单段数码管
    turtle.pendown() if draw else turtle.penup()
    turtle.fd(40)
    turtle.right(90)


def drawDigit(digit):  # 根据数字绘制七段数码管
    drawLine(True) if digit in [2, 3, 4, 5, 6, 8, 9] else drawLine(False)
    drawLine(True) if digit in [0, 1, 3, 4, 5, 6, 7, 8, 9] else drawLine(False)
    drawLine(True) if digit in [0, 2, 3, 5, 6, 8, 9] else drawLine(False)
    drawLine(True) if digit in [0, 2, 6, 8] else drawLine(False)
    turtle.left(90)
    drawLine(True) if digit in [0, 4, 5, 6, 8, 9] else drawLine(False)
    drawLine(True) if digit in [0, 2, 3, 5, 6, 7, 8, 9] else drawLine(False)
    drawLine(True) if digit in [0, 1, 2, 3, 4, 7, 8, 9] else drawLine(False)
    turtle.left(180)
    turtle.penup()
    turtle.fd(20)


def drawDate(date):  # 获得要输出的数字
    for i in date:
        drawDigit(eval(i))  # 通过eval()函数将数字变为整数


def main():
    turtle.setup(800, 350, 200, 200)
    turtle.penup()
    turtle.fd(-300)
    turtle.pensize(5)
    drawDate("20181010")
    turtle.hideturtle()
    turtle.done()


main()
```

```py [SevenDigitsDrawV2.py]
# SevenDigitsDrawV2.py
import turtle, time


def drawGap():  # 绘制数码管间隔
    turtle.penup()
    turtle.fd(5)


def drawLine(draw):  # 绘制单段数码管
    drawGap()
    turtle.pendown() if draw else turtle.penup()
    turtle.fd(40)
    drawGap()
    turtle.right(90)


def drawDigit(d):  # 根据数字绘制七段数码管
    drawLine(True) if d in [2, 3, 4, 5, 6, 8, 9] else drawLine(False)
    drawLine(True) if d in [0, 1, 3, 4, 5, 6, 7, 8, 9] else drawLine(False)
    drawLine(True) if d in [0, 2, 3, 5, 6, 8, 9] else drawLine(False)
    drawLine(True) if d in [0, 2, 6, 8] else drawLine(False)
    turtle.left(90)
    drawLine(True) if d in [0, 4, 5, 6, 8, 9] else drawLine(False)
    drawLine(True) if d in [0, 2, 3, 5, 6, 7, 8, 9] else drawLine(False)
    drawLine(True) if d in [0, 1, 2, 3, 4, 7, 8, 9] else drawLine(False)
    turtle.left(180)
    turtle.penup()
    turtle.fd(20)


def drawDate(date):
    turtle.pencolor("red")
    for i in date:
        if i == "-":
            turtle.write("年", font=("Arial", 18, "normal"))
            turtle.pencolor("green")
            turtle.fd(40)
        elif i == "=":
            turtle.write("月", font=("Arial", 18, "normal"))
            turtle.pencolor("blue")
            turtle.fd(40)
        elif i == "+":
            turtle.write("日", font=("Arial", 18, "normal"))
        else:
            drawDigit(eval(i))


def main():
    turtle.setup(800, 350, 200, 200)
    turtle.penup()
    turtle.fd(-350)
    turtle.pensize(5)
    #    drawDate('2018-10=10+')
    drawDate(time.strftime("%Y-%m=%d+", time.gmtime()))
    turtle.hideturtle()
    turtle.done()


main()
```

:::

### 2.8. 科赫雪花小包裹

::: code-group

```py [KochDrawV1.py]
# KochDrawV1.py
import turtle


def koch(size, n):
    if n == 0:
        turtle.fd(size)
    else:
        for angle in [0, 60, -120, 60]:
            turtle.left(angle)
            koch(size / 3, n - 1)


def main():
    turtle.setup(800, 400)
    turtle.penup()
    turtle.goto(-300, -50)
    turtle.pendown()
    turtle.pensize(2)
    koch(600, 3)  # 0阶科赫曲线长度，阶数
    turtle.hideturtle()
    turtle.done()


main()
```

```py [KochDrawV2.py]
# KochDrawV2.py
import turtle


def koch(size, n):
    if n == 0:
        turtle.fd(size)
    else:
        for angle in [0, 60, -120, 60]:
            turtle.left(angle)
            koch(size / 3, n - 1)


def main():
    turtle.setup(600, 600)
    turtle.penup()
    turtle.goto(-200, 100)
    turtle.pendown()
    turtle.pensize(2)
    level = 3  # 3阶科赫雪花，阶数
    koch(400, level)
    turtle.right(120)
    koch(400, level)
    turtle.right(120)
    koch(400, level)
    turtle.hideturtle()
    turtle.done()


main()
```

:::

### 2.9. 基本统计值计算

::: code-group

```py [CalStatisticsV1.py]
# CalStatisticsV1.py
def getNum():  # 获取用户不定长度的输入
    nums = []
    iNumStr = input("请输入数字(回车退出): ")
    while iNumStr != "":
        nums.append(eval(iNumStr))
        iNumStr = input("请输入数字(回车退出): ")
    return nums


def mean(numbers):  # 计算平均值
    s = 0.0
    for num in numbers:
        s = s + num
    return s / len(numbers)


def dev(numbers, mean):  # 计算方差
    sdev = 0.0
    for num in numbers:
        sdev = sdev + (num - mean) ** 2
    return pow(sdev / (len(numbers) - 1), 0.5)


def median(numbers):  # 计算中位数
    sorted(numbers)
    size = len(numbers)
    if size % 2 == 0:
        med = (numbers[size // 2 - 1] + numbers[size // 2]) / 2
    else:
        med = numbers[size // 2]
    return med


n = getNum()  # 主体函数
m = mean(n)
print("平均值:{},方差:{:.2},中位数:{}.".format(m, dev(n, m), median(n)))

"""
请输入数字(回车退出): 1
请输入数字(回车退出): 2
请输入数字(回车退出): 3
请输入数字(回车退出): 4
请输入数字(回车退出): 5
请输入数字(回车退出):
平均值:3.0,方差:1.6,中位数:3.
"""
```

:::

### 2.10. 文本词频统计

::: code-group

```py [CalThreeKingdomsV1.py]
# CalThreeKingdomsV1.py
import jieba

txt = open("threekingdoms.txt", "r", encoding="utf-8").read()
words = jieba.lcut(txt)
counts = {}
for word in words:
    if len(word) == 1:
        continue
    else:
        counts[word] = counts.get(word, 0) + 1
items = list(counts.items())
items.sort(key=lambda x: x[1], reverse=True)
for i in range(15):
    word, count = items[i]
    print("{0:<10}{1:>5}".format(word, count))

"""
曹操          953
孔明          836
将军          772
却说          656
玄德          585
关公          510
丞相          491
二人          469
不可          440
荆州          425
玄德曰         390
孔明曰         390
不能          384
如此          378
张飞          358
"""
```

```py [CalThreeKingdomsV2.py]
# CalThreeKingdomsV2.py
import jieba

excludes = {"将军", "却说", "荆州", "二人", "不可", "不能", "如此"}
txt = open("threekingdoms.txt", "r", encoding="utf-8").read()
words = jieba.lcut(txt)
counts = {}
for word in words:
    if len(word) == 1:
        continue
    elif word == "诸葛亮" or word == "孔明曰":
        rword = "孔明"
    elif word == "关公" or word == "云长":
        rword = "关羽"
    elif word == "玄德" or word == "玄德曰":
        rword = "刘备"
    elif word == "孟德" or word == "丞相":
        rword = "曹操"
    else:
        rword = word
    counts[rword] = counts.get(rword, 0) + 1
for word in excludes:
    del counts[word]
items = list(counts.items())
items.sort(key=lambda x: x[1], reverse=True)
for i in range(10):
    word, count = items[i]
    print("{0:<10}{1:>5}".format(word, count))

"""
曹操         1451
孔明         1383
刘备         1252
关羽          784
张飞          358
商议          344
如何          338
主公          331
军士          317
吕布          300
"""
```

```py [CalHamletV1.py]
# CalHamletV1.py
def getText():
    txt = open("hamlet.txt", "r").read()
    txt = txt.lower()
    for ch in '!"#$%&()*+,-./:;<=>?@[\\]^_‘{|}~':
        txt = txt.replace(ch, " ")  # 将文本中特殊字符替换为空格
    return txt


hamletTxt = getText()
words = hamletTxt.split()
counts = {}
for word in words:
    counts[word] = counts.get(word, 0) + 1
items = list(counts.items())
items.sort(key=lambda x: x[1], reverse=True)
for i in range(10):
    word, count = items[i]
    print("{0:<10}{1:>5}".format(word, count))

"""
the        1138
and         965
to          754
of          669
you         550
i           542
a           542
my          514
hamlet      462
in          436
"""
```

:::

### 2.11. 自动轨迹绘制

::: code-group

```py [AutoTraceDraw.py]
# AutoTraceDraw.py
import turtle as t

t.title("自动轨迹绘制")
t.setup(800, 600, 0, 0)
t.pencolor("red")
t.pensize(5)
# 数据读取
datals = []
f = open("data.txt")
for line in f:
    line = line.replace("\n", "")
    datals.append(list(map(eval, line.split(","))))
f.close()
# 自动绘制
for i in range(len(datals)):
    t.pencolor(datals[i][3], datals[i][4], datals[i][5])
    t.fd(datals[i][0])
    if datals[i][1]:
        t.rt(datals[i][2])
    else:
        t.lt(datals[i][2])

t.done()
```

```txt [data.txt]
300,0,144,1,0,0
300,0,144,0,1,0
300,0,144,0,0,1
300,0,144,1,1,0
300,0,108,0,1,1
184,0,72,1,0,1
184,0,72,0,0,0
184,0,72,0,0,0
184,0,72,0,0,0
184,1,72,1,0,1
184,1,72,0,0,0
184,1,72,0,0,0
184,1,72,0,0,0
184,1,72,0,0,0
184,1,720,0,0,0
```

:::

### 2.12. 政府工作报告词云

::: code-group

```py [GovRptWordCloudv1T1.py]
# GovRptWordCloudv1.py
import jieba
import wordcloud

f = open("新时代中国特色社会主义.txt", "r", encoding="utf-8")

t = f.read()
f.close()
ls = jieba.lcut(t)

txt = " ".join(ls)
w = wordcloud.WordCloud(
    width=1000, height=700, background_color="white", font_path="msyh.ttc"
)
w.generate(txt)
w.to_file("grwordcloud.png")
```

```py [GovRptWordCloudv1T2.py]
# GovRptWordCloudv1.py
import jieba
import wordcloud

f = open("关于实施乡村振兴战略的意见.txt", "r", encoding="utf-8")

t = f.read()
f.close()
ls = jieba.lcut(t)

txt = " ".join(ls)
w = wordcloud.WordCloud(
    width=1000, height=700, background_color="white", font_path="msyh.ttc"
)
w.generate(txt)
w.to_file("grwordcloud.png")
```

```py [GovRptWordCloudv1T3.py]
# GovRptWordCloudv1.py
import jieba
import wordcloud

f = open("新时代中国特色社会主义.txt", "r", encoding="utf-8")

t = f.read()
f.close()
ls = jieba.lcut(t)

txt = " ".join(ls)
w = wordcloud.WordCloud(
    width=1000, height=700, background_color="white", font_path="msyh.ttc", max_words=15
)
w.generate(txt)
w.to_file("grwordcloud.png")
```

```py [GovRptWordCloudv1T4.py]
# GovRptWordCloudv1.py
import jieba
import wordcloud

f = open("关于实施乡村振兴战略的意见.txt", "r", encoding="utf-8")

t = f.read()
f.close()
ls = jieba.lcut(t)

txt = " ".join(ls)
w = wordcloud.WordCloud(
    width=1000, height=700, background_color="white", font_path="msyh.ttc", max_words=15
)
w.generate(txt)
w.to_file("grwordcloud.png")
```

```py [GovRptWordCloudv2T1.py]
# GovRptWordCloudv2.py
import jieba
import wordcloud
from imageio import imread

mask = imread("fivestart.png")
excludes = {}
f = open("新时代中国特色社会主义.txt", "r", encoding="utf-8")
t = f.read()
f.close()
ls = jieba.lcut(t)
txt = " ".join(ls)
w = wordcloud.WordCloud(
    width=1000, height=700, background_color="white", font_path="msyh.ttc", mask=mask
)
w.generate(txt)
w.to_file("grwordcloudm.png")
```

```py [GovRptWordCloudv2T2.py]
# GovRptWordCloudv2.py
import jieba
import wordcloud
from imageio import imread

mask = imread("fivestart.png")
excludes = {}
f = open("关于实施乡村振兴战略的意见.txt", "r", encoding="utf-8")
t = f.read()
f.close()
ls = jieba.lcut(t)
txt = " ".join(ls)
w = wordcloud.WordCloud(
    width=1000, height=700, background_color="white", font_path="msyh.ttc", mask=mask
)
w.generate(txt)
w.to_file("grwordcloudm.png")
```

```py [GovRptWordCloudv2T3.py]
# GovRptWordCloudv2.py
import jieba
import wordcloud
from imageio import imread

mask = imread("chinamap.jpg")
excludes = {}
f = open("新时代中国特色社会主义.txt", "r", encoding="utf-8")
t = f.read()
f.close()
ls = jieba.lcut(t)
txt = " ".join(ls)
w = wordcloud.WordCloud(
    width=1000, height=700, background_color="white", font_path="msyh.ttc", mask=mask
)
w.generate(txt)
w.to_file("grwordcloudm.png")
```

```py [GovRptWordCloudv2T4.py]
# GovRptWordCloudv2.py
import jieba
import wordcloud
from imageio import imread

mask = imread("chinamap.jpg")
excludes = {}
f = open("关于实施乡村振兴战略的意见.txt", "r", encoding="utf-8")
t = f.read()
f.close()
ls = jieba.lcut(t)
txt = " ".join(ls)
w = wordcloud.WordCloud(
    width=1000, height=700, background_color="white", font_path="msyh.ttc", mask=mask
)
w.generate(txt)
w.to_file("grwordcloudm.png")
```

:::

### 2.13. 体育竞技分析

::: code-group

```py [MatchAnalysis.py]
# MatchAnalysis.py
from random import random


def printIntro():
    print("这个程序模拟两个选手A和B的某种竞技比赛")
    print("程序运行需要A和B的能力值（以0到1之间的小数表示）")


def getInputs():
    a = eval(input("请输入选手A的能力值(0-1): "))
    b = eval(input("请输入选手B的能力值(0-1): "))
    n = eval(input("模拟比赛的场次: "))
    return a, b, n


def simNGames(n, probA, probB):
    winsA, winsB = 0, 0
    for i in range(n):
        scoreA, scoreB = simOneGame(probA, probB)
        if scoreA > scoreB:
            winsA += 1
        else:
            winsB += 1
    return winsA, winsB


def gameOver(a, b):
    return a == 15 or b == 15


def simOneGame(probA, probB):
    scoreA, scoreB = 0, 0
    serving = "A"
    while not gameOver(scoreA, scoreB):
        if serving == "A":
            if random() < probA:
                scoreA += 1
            else:
                serving = "B"
        else:
            if random() < probB:
                scoreB += 1
            else:
                serving = "A"
    return scoreA, scoreB


def printSummary(winsA, winsB):
    n = winsA + winsB
    print("竞技分析开始，共模拟{}场比赛".format(n))
    print("选手A获胜{}场比赛，占比{:0.1%}".format(winsA, winsA / n))
    print("选手B获胜{}场比赛，占比{:0.1%}".format(winsB, winsB / n))


def main():
    printIntro()
    probA, probB, n = getInputs()
    winsA, winsB = simNGames(n, probA, probB)
    printSummary(winsA, winsB)


main()

"""
这个程序模拟两个选手A和B的某种竞技比赛
程序运行需要A和B的能力值（以0到1之间的小数表示）
请输入选手A的能力值(0-1): 0.5
请输入选手B的能力值(0-1): 0.5
模拟比赛的场次: 1000
竞技分析开始，共模拟1000场比赛
选手A获胜548场比赛，占比54.8%
选手B获胜452场比赛，占比45.2%

这个程序模拟两个选手A和B的某种竞技比赛
程序运行需要A和B的能力值（以0到1之间的小数表示）
请输入选手A的能力值(0-1): 0.5
请输入选手B的能力值(0-1): 0.5
模拟比赛的场次: 1000
竞技分析开始，共模拟1000场比赛
选手A获胜499场比赛，占比49.9%
选手B获胜501场比赛，占比50.1%
"""
```

:::

### 2.14. 第三方库安装脚本

::: code-group

```py [BatchInstall.py]
# BatchInstall.py
import os

libs = {
    "numpy",
    "matplotlib",
    "pillow",
    "sklearn",
    "requests",
    "jieba",
    "beautifulsoup4",
    "wheel",
    "networkx",
    "sympy",
    "pyinstaller",
    "django",
    "flask",
    "werobot",
    "pyqt5",
    "pandas",
    "pyopengl",
    "pypdf2",
    "docopt",
    "pygame",
}
try:
    for lib in libs:
        os.system("pip3 install " + lib)
    print("Successful")
except:
    print("Failed Somehow")
```

:::

### 2.15. 霍兰德人格分析雷达图

::: code-group

```py [HollandRadarDraw.py]
# HollandRadarDraw
import numpy as np
import matplotlib.pyplot as plt
import matplotlib

matplotlib.rcParams["font.family"] = "Hiragino Sans GB"

radar_labels = np.array(
    ["研究型(I)", "艺术型(A)", "社会型(S)", "企业型(E)", "常规型(C)", "现实型(R)", "研究型(I)"]
)  # 雷达标签，增加一个起始元素以与 angles 数组长度匹配
nAttr = 6
data = np.array(
    [
        [0.40, 0.32, 0.35, 0.30, 0.30, 0.88],
        [0.85, 0.35, 0.30, 0.40, 0.40, 0.30],
        [0.43, 0.89, 0.30, 0.28, 0.22, 0.30],
        [0.30, 0.25, 0.48, 0.85, 0.45, 0.40],
        [0.20, 0.38, 0.87, 0.45, 0.32, 0.28],
        [0.34, 0.31, 0.38, 0.40, 0.92, 0.28],
    ]
)  # 数据值
data_labels = ("艺术家", "实验员", "工程师", "推销员", "社会工作者", "记事员")
angles = np.linspace(0, 2 * np.pi, nAttr, endpoint=False)
data = np.concatenate((data, [data[0]]))
angles = np.concatenate((angles, [angles[0]]))
fig = plt.figure(facecolor="white")
plt.subplot(111, polar=True)
plt.plot(angles, data, "o-", linewidth=1, alpha=0.2)
plt.fill(angles, data, alpha=0.25)
plt.thetagrids(angles * 180 / np.pi, radar_labels)  # 移除 frac 参数
plt.figtext(0.52, 0.95, "霍兰德人格分析", ha="center", size=20)
legend = plt.legend(data_labels, loc=(0.94, 0.80), labelspacing=0.1)
plt.setp(legend.get_texts(), fontsize="large")
plt.grid(True)
plt.savefig("holland_radar.jpg")
plt.show()

```

:::

### 2.16. 玫瑰花绘制

::: code-group

```py [RoseDraw.py]
# RoseDraw.py
import turtle as t


# 定义一个曲线绘制函数
def DegreeCurve(n, r, d=1):
    for i in range(n):
        t.left(d)
        t.circle(r, abs(d))


# 初始位置设定
s = 0.2  # size
t.setup(450 * 5 * s, 750 * 5 * s)
t.pencolor("black")
t.fillcolor("red")
t.speed(100)
t.penup()
t.goto(0, 900 * s)
t.pendown()
# 绘制花朵形状
t.begin_fill()
t.circle(200 * s, 30)
DegreeCurve(60, 50 * s)
t.circle(200 * s, 30)
DegreeCurve(4, 100 * s)
t.circle(200 * s, 50)
DegreeCurve(50, 50 * s)
t.circle(350 * s, 65)
DegreeCurve(40, 70 * s)
t.circle(150 * s, 50)
DegreeCurve(20, 50 * s, -1)
t.circle(400 * s, 60)
DegreeCurve(18, 50 * s)
t.fd(250 * s)
t.right(150)
t.circle(-500 * s, 12)
t.left(140)
t.circle(550 * s, 110)
t.left(27)
t.circle(650 * s, 100)
t.left(130)
t.circle(-300 * s, 20)
t.right(123)
t.circle(220 * s, 57)
t.end_fill()
# 绘制花枝形状
t.left(120)
t.fd(280 * s)
t.left(115)
t.circle(300 * s, 33)
t.left(180)
t.circle(-300 * s, 33)
DegreeCurve(70, 225 * s, -1)
t.circle(350 * s, 104)
t.left(90)
t.circle(200 * s, 105)
t.circle(-500 * s, 63)
t.penup()
t.goto(170 * s, -30 * s)
t.pendown()
t.left(160)
DegreeCurve(20, 2500 * s)
DegreeCurve(220, 250 * s, -1)
# 绘制一个绿色叶子
t.fillcolor("green")
t.penup()
t.goto(670 * s, -180 * s)
t.pendown()
t.right(140)
t.begin_fill()
t.circle(300 * s, 120)
t.left(60)
t.circle(300 * s, 120)
t.end_fill()
t.penup()
t.goto(180 * s, -550 * s)
t.pendown()
t.right(85)
t.circle(600 * s, 40)
# 绘制另一个绿色叶子
t.penup()
t.goto(-150 * s, -1000 * s)
t.pendown()
t.begin_fill()
t.rt(120)
t.circle(300 * s, 115)
t.left(75)
t.circle(300 * s, 100)
t.end_fill()
t.penup()
t.goto(430 * s, -1070 * s)
t.pendown()
t.right(30)
t.circle(-600 * s, 35)
t.done()
```

:::

## 3. 常见问题

::: tip 💡 提示

这一部分信息主要来自于 Mooc 教程的首页简介中。

![img](https://cdn.jsdelivr.net/gh/tnotesjs/imgs-2026@main/2026-08-20-17-21-24.png)

:::

### 3.1. Python 语言、C 语言、Java 语言、VB 语言…… 到底哪种适合作为入门编程语言呢？

- Python 是最好的程序设计入门语言、也是最先进的程序设计语言。
- 如果只想学一门程序设计语言，请学 Python；如果想学一门最先进的程序设计语言，请学 Python。
- 更多教学讨论请参考：
  - “Python 语言: 程序设计课程教学改革的理想选择”，《中国大学教学》，2016 年第 2 期
  - [https://d.wanfangdata.com.cn/Periodical/zgdxjx201602010](https://d.wanfangdata.com.cn/Periodical/zgdxjx201602010)

### 3.2. Python 2.x 和 Python 3.x，该学习哪个版本？

- Python 3.x，本课程及嵩老师所有 Python 课程只讲授这个版本。
- 与传统软件升级不同，3.x 版本与 2.x 版本并不兼容，3.x 版本 2008 年发布，至今，所有 Python 主流功能库都可以稳定且更高效地运行在 Python 3.x 版本下，专业 Python 程序员都已经使用 Python 3.x 版本，无可争议。

### 3.3. Python 语言是跨平台的吗？

- Python 语言所编写程序可以无需修改在 Windows、Linux、UNIX、Mac 等操作系统上使用。
- 严谨些：如果 Python 程序所调用的库是平台无关的，则可以跨平台。

### 3.4. Python 语言是面向对象语言吗？

- 面向对象是程序设计方法的一种，Python 语言并不局限于此。
- 你可以学习面向对象程序设计方法，并利用 Python 语言实现，也可以仅仅用面向过程的基本方式，甚至，你可以没有任何风格的写几行代码，Python 语言都是支持的。它就是这么任性！

### 3.5. 在线开放课程只能看到视频，有问题谁来解答？

- 编程能力是一技之长，学习过程中遇到问题很正常，为了更好地为同学们服务，本课程由教师和至少 3 名助教每天在线上答疑，很多同学也会在线上回答所提出的问题，一般问题在几个小时内可以得到解决。

### 3.6. 这个课程需要配套教材或工具书吗？

- 本课程将提供视频、文本资料和程序代码等作为学习资料，提供 Python123 平台进行实践训练。
- 同学们可以选择使用或不使用教材。当然，一本好书，事半功倍，建议选择一本教材，有助于更系统掌握 Python 语言。尽公不避嫌，嵩老师的第 2 版教材内容丰富，相当值得拥有。

### 3.7. 全国计算机等级考试二级 Python 科目有什么用？需要参加吗？

- 全国计算机等级考试二级（简称：等考）由教育部考试中心（高考、四六级和研究生考试也是这个官方部门组织的哦！）组织，主要面向高校学生及社会学习者开展的水平性考试，其中 Python 语言课目于 2018 年 9 月首次开考，每年 3 月和 9 月两次大考。
- 等考对计算机专业学生没有太大意义，毕竟专业学生需要很专业；但对于非计算机专业学生证明计算机尤其是编程水平非常权威也比较有用。据说上海市落户的积分政策中有对计算机水平及等级考试的要求。

### 3.8. 这门 Python 语言课程来源于哪里？质量如何呢？

- Python 教学没有太多成熟经验可供参考，我们团队一直与国外在同期探索，不断演进并优化课程内容。发展不停步、质量总有进步吧 <sup>\_</sup>
- 2009 年，美国一些大学开始开设 Python 课程，替换 Java 等编程语言，国外教学中产生的成熟有效经验较少；
- 2013 年，北京理工大学率先在国内开设 Python 课程，设计了首套 Python 语言 v1.0 大纲，受当时国外教学经验影响，该版本大纲比较传统；
- 2014 年，团队提出围绕 “计算生态” 的 v2.0 版本大纲，大尺度原创内容，并在校内课程教学中试行，效果显著；
- 2015 年，本课程上线，使用第一套视频，讲解优化后的 v2.1 版本大纲，起到了向全国高校推广 Python 语言教学的作用，但受限于 MOOC 经验不足，留下了许多遗憾；
- 2016 年，团队正式提出 “理解和运用计算生态” 的教学理念，构建了 v3.0 版本大纲，原创性提出了 “Python 基础语法” 体系，并在校内课程试行，同期推广全国，教学效果显著；
- 2017 年，团队历经 2 年，经过 3 次推翻、2 次重写后，正式出版了遵照 v3.0 版本大纲的《Python 语言程序设计基础 (第 2 版)》新形态教材；
- 2018 年，本课程大! 尺! 度! 更新上线，采用使用全新的第二套视频，采用优化后的 v3.2 版本大纲。

### 3.9. 为什么开课团队这么执着于 Python 课程大纲及所谓的 “课程大纲版本”？

- 程序员就这点儿爱好，定个 v1.0 版本不断迭代，程序员兼教师们也都不能免俗 <sup>\_</sup>
- 更为重要地，作为教师，我们深刻认识到 “知识体系” 和“课程体系”的重要性。
- “知识体系” 是帮助学习者快速获得某领域认知、知识和技术能力的关键，相比网络碎片化知识点学习，体系化才是真正的捷径；
- “课程体系” 是帮助学习者在符合认知规律条件下快速掌握 “知识体系” 的一个过程，构建一个有效的课程体系需要相当的实践和无数的教训。
- 对于 Python 课程，“知识体系” 和 “课程体系” 在几年前都不具备。从 2013 年开始，我们将两个体系合并研究，形成 “课程大纲”，不断构建、试错和优化，以版本形式进行迭代，努力为学习者提供 “最好效果、最高质量” 的教学内容和形式。直到今天，教训很多，经验略有，仍在努力...

## 4. 引用

- [中国大学MOOC][1]
- [Python语言程序设计][2]
- [Python 官网][3]
- [Python123 学习网站][4]
- [TNotes.yuque][5]

[1]: https://www.icourse163.org/
[2]: https://www.icourse163.org/course/BIT-268001
[3]: https://www.python.org
[4]: https://python123.io
[5]: https://www.yuque.com/tdahuyou/tnotes.yuque
