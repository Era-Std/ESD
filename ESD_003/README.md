# ESD 003-Code Specification (Golang)  

<a href="./zh_README.md">简体中文</a>

## What is a code specification  
Code specifications make the code of a project easier to read...  

### File Naming  
_Although it is not too restrictive, a simple naming convention is still needed_  
_Snake name:_ `package name_function name`::for example: `foo_bar`  
_Hump naming:_ `Function name` (big hump):: For example: `FooBar`  

### Constant name  
_Old code style_  
Constant naming we use all uppercase snake naming: for example `FOO_BAR_DOG_CAT`  

### Variable name  
_Extremely modern style_  
For variable naming, we use small camel case naming:: For example, `fooBarDogCat`  

### Package name  
_A naming art_  
The package name should not be based on **keywords** such as `types` `mains`  
It is generally recommended to use the big hump to name a package or use the snake-shaped name (the all-caps snake-shaped naming method is not allowed)  
Good example: `FooBar`  

### Function name  
_Modern code style_  
The function name should represent the function of this function, it is not allowed to include the package name, use the big/small hump name  
Good example: `CreateADog` `removeACat`  

### Struct  
_Look, this stuff is like writing poetry_  
The naming of the structure should represent the role of this structure, use big/small hump naming, and do not conflict with _package name/variable name/function name/file name_ in the project  
Good example:  
```golang
Protocol struct {
Header []byte
Body []byte
Signature []byte
}
```

### Code format
_Maybe this is the real writer_  
It is recommended to use tab indentation. If it contains symbols such as curly braces, the next line of code needs to be indented on the basis of the previous line of code.  
Good example:  
```golang
package foo

func bar(args string) string {
    if(args == "dog") {
        return "cat"
    }
    return "dog"
}
```

## Simple demo
```golang
package main

import(
    "fmt"
)

type Output struct {
    Text string
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
