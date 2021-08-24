# ESD 003-代码规范(Golang)

## 什么是代码规范
代码规范能让一个项目的代码更加容易的阅读...

### 文件命名
_虽然并没有太大的限制但还是需要一个简单的命名规范_
_蛇形命名:_ `包名_功能名`::例如: `foo_bar`
_驼峰命名:_ `功能名`(大驼峰)::例如: `FooBar`

### 常量名
_古老的代码风格_
常量命名我们使用全大写的蛇形命名::例如`FOO_BAR_DOG_CAT`

### 变量名
_极具现代化的风格_
变量命名我们使用小驼峰命名::例如`fooBarDogCat`

### 包名
_一种命名艺术_
包名不应该建立在**关键词**的基础上比如`types` `mains`
一般建议使用大驼峰命名一个包亦可以使用蛇形命名(不允许使用全大写蛇形的命名方法)
良好的例子: `FooBar`

### 函数名
_现代化的代码风格_
函数名应代表了这个函数的作用,不允许包含包名,使用大/小驼峰命名
良好的例子: `CreateADog` `removeACat`

### 结构体
_看,这玩意跟写诗一样_
结构体的命名应代表了这个结构体的作用,使用大/小驼峰命名,不与项目中的 _包名/变量名/函数名/文件名_ 冲突
良好的例子: 
```golang
Protocol struct {
	Header 		[]byte
	Body		[]byte
	Signature 	[]byte
}
```

### 代码格式
_也许这才是真正的作家吧_
建议使用tab缩进,如果包含花括号之类的符号则下一行代码需要在上一行代码的基础上进行缩进
良好的例子:
```golang
package foo

func bar(args string) string {
    if(args == "dog") {
        return "cat"
    }
    return "dog"
}
```

## 简单的演示
```golang
package main

import(
    "fmt"
)

type Output struct {
    Text    string
}

var foo = "Bar"

const FOO_BAR string = "hello,world"

func Dog() int {
    var myWorld Output
    myWorld.Text = foo
    if(myWorld.Text != FOO_BAR){
        fmt.Println(myWorld.Text)
        return 0
    }
    fmt.Println(FOO_BAR)
    return 1
}

func main() {
    Dog()
}
```
