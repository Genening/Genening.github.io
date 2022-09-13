---
title: perl_language
author: Genening
# thumbnail: /gallery/thumbnail/
date: 2021-07-22 15:22:10
updated: 2021-07-22 15:22:10
categories: Linux
tags: perl
---

## 前言
最近在学习Linux系统，Perl是Linux上常用的开发语言，和Linux中的shell script有很多相似之处，可以很方便地处理文本数据，也能够很好地支持正则，并且拥有齐全的工具库和优秀的社区，因此，比起Linux shell script而言，Perl功能更强大而且更好编写，所以为了能够更好地使用Linux完成工作任务，Perl值得一学。

<!--more-->

## 1.perl基本知识
* 非常适合用于文本处理并生成更多文本
* 语法宽松，可以自己增强要求
* 强制严格语法
```
use strict;
use warning;
```
* 脚本式运行，无交互式
* 弱类型  不区分变量内容是数字还是字符串，只有当使用的时候才会编译器自动判断
* 区分字符串操作符（gt/lt/eq等）和数值操作符（==  <=  >=等），与shell script设定类似


## 2.变量类型
1. scalar（标量）

```
my $scalar = 1
```

2. array（数组）  用@array 声明变量，没有限制长度，超出长度的索引会返回undef

```
my @array = ("hello", "world", "hi", "friend")   #用小括号()声明一个array
my $arrayRef = ["hello", "world", "hi", "friend"] #用中括号[]声明一个引用
```
* $#var   内置值，表示数组的最后一位
* 方法：pop/push/shift/unshift/splice
* reverse()
* map()
* grep()
* sort @array
3. hash（哈希）  

```
my %hash = (
    "Newton" => value1,
    "Enistan" => value2
);   #用小括号()声明hash类型
```
```
my $hashRef = {
    "Newton" => value1,
    "Enistan" => value2
}  #用大括号{}声明hash引用

my @k = keys  %hash    返回keys列表
my @v = values %hash  返回values的列表

exists %hash{'key'}   判断'key'在不在hash中
delete $hash{'key'}   删除hash中键值对
```
4. string（字符串）
```
$string = "strings"
join()
reverse()
```
5. list（列表）----数组、字符串、哈希

* (value1, value2, 'value3', 4)   这种形式就是列表
* boolean（布尔值）  perl中没有布尔值，只有一些特定的内容会被认为是false，如0/""/undef

## 3.常用函数
* chomp($variable)   去除字符串末尾换行符\n
* split($variable)   默认分割符\s+
* index()
* join()
* map()
* reverse()  用在字符串上会将字符串按单个字母进行逆转
* splice()
* grep()


## 4.上下文——perl最大特点，代码上下文/语境敏感，通过上下文判断表意
* 字符串上下文   前一个变量或函数期待一个字符串返回，后一句话就会返回一个字符串
* 数组上下文    前一个变量或函数期待一个数组返回，后一句话就会返回一个数组
* 哈希上下文 前一个变量或函数期待一个哈希返回，后一句话就会返回一个哈希
* print reverse "hello world"     因为print期待一个列表输入，所以reverse会返回一个列表结果
* print scalar reverse "hello world"  因为scalar期待一个字符串输入，所以reverse会返回一个字符串结果


## 5.作用域---命名代码块、匿名代码块
* 代码块中可以操作全局变量，进行修改，修改会保存到全局
* 如果代码块中重新声明一个与全局变量相同的变量，两者互相独立，作用域不同
* 代码块可以命名，意义在于格式更清晰；整个程序相当于一个全局的匿名代码块


## 6.引用
* 相当于是个标量
* 引用可以嵌套
```
my $arrayRef = \@array     #用反斜杠来引用
print $($arrayRef)
my $hashRef = \%hash
print %{$hashRef{"hash"} [0]}  #返回引用里的第一个hash引用的hash类型本身
print $hashRef{"hash"} -> [1] -> "name"   #返回第二个引用中的第一个值scalar
my $scalarRef = \$scalar
```
引用可以用于面向对象编程，可以构造复杂的数据结构满足需求

## 7.流程控制
1. 条件判断
```
if(){....}elsif(){....}else{}

unless(){}else{}

print "you have", $eggs == 0 ? "no eggs":  $eggs == 1? "an egg": "some eggs";
```

2. 循环控制

```
while(){}

until(){}

for(my $i = 0; $i <=30; $i++){}

do{}while()

for my $key (keys %scientists){}

next/last   #等价于其他语言中continue/break
```


## 8. perl正则三种形式（匹配、替换、转换）

* =~  表示匹配   !~ 表示不匹配
* m/pattern/
* s/pattern/subsitution/
* tr/pattern/transformation/

```
my $string = "~~Hello World~~"

if($string =~ m/(\w+)\s+(\w+)/){
    print "success\n"
}  # string 中匹配上的内容会存储到默认的变量序列里 $1/$2/$3....

print "$1\n"  # Hello
print "$2\n"  # World
```

* $`  匹配区间前面的非匹配部分内容

* $&  匹配区间内的匹配部分内容

* $'  匹配区间后面的非匹配部分内容

* 修饰符：i/o/s/g 

### 更多正则表达式

`.   x?  x*  x+  .*  .+  .?  {m} {m, n} {m, }  [] [^] `

这些正则表达式是对基本正则符号的扩展，可以让正则的匹配功能更强大。其实正则的理解可以分为两部分，一部分是字符匹配，另一部分是次数匹配。字符匹配指的是通过正则表达式匹配一个特定的字符，不管是字母/数字/打印字符/空白字符等等内容，这些都是明确的字符对象，我们可以通过字符匹配正则表达式去匹配他们；次数匹配指的是我们指定字符匹配的发生次数，例如我们在字符匹配中要匹配10个字母字符，我们不用也不必要把同样的字符匹配正则表达式重复写10次，我们只需要添加一个次数匹配正则表达式即可，比如{10}即可指定匹配10次，当然还有其它的一些特定的指定方法，比如? * +分别表示不同的匹配次数。


## 9.文件操作

* 保留字 STDIN   STDOUT   STDERR   DATA   ARGV   ARGVOUT
* 文件句柄是perl中程序与外界IO操作的名称
```
my $file = "text.txt";
my $out_file = "out.txt";
my $log_file = "log.txt";

open IN1, "$file";
open IN2, "< $file";
open IN3, "<", "$file";
open OUT1, "> $out_file";
open OUT2, ">> $out_file";
close IN1
```
* 文件测试

|表达式|描述|
|:----|:----|
|-e|是否存在|
|-s|是否存在且有内容|
|-d|是否目录|
|-f|是否文本|
|-r|是否可读|
|-w|是否可写|


### 拓展
perl中也同样有系统调用、子程序、模块，这些内容倒是和Python并无两异，因此不用太多纠结，理解即可。

## 结语
这一次的学习是从零开始学习的，之前我并没有perl的编程经验，当然，我有着丰富的Python编程经验，因此基础比较扎实。在这一次的学习过程中，很明显地感觉到在学习一门新的语言时，应该把握的重点是一门语言的数据类型或者说数据结构。数据结构的功能范围决定了我们怎么去使用一门语言，它决定了我们怎么获取数据、控制数据流和数据输出。因此，当我们把握了一门新语言的数据结构内容，那么我们就可以自信地说，我们已经基本掌握了这门新语言了，接下来要做的就是在日常生活的练习中，不断掌握更多的内置方法和基本技巧，直至不断达到更高的编程水平。

* 数据类型定义
* 数据结构定义与使用方法
* 文件操作（读入与写出）

这一次的经历给我的更大的启发是，对于一个编程小白而言，学习编程的真正难点并不是基本的语法规则，而是从零开始去理解和使用一门语言的数据结构内容，基本的语法规则经过短期的重复训练我们便可以熟记于心，不会是我们学习编程的太大困扰，但是对于一门编程语言的数据结构的理解就没这么简单，不过，值得庆幸的是，虽然数据结构可以很复杂，学习比较困难，但是，简单地学习一门编程语言的使用不需要太深层次的掌握，能基本理解即可。





