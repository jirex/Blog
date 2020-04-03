+++
title = "Go基础"
author = ["jirex"]
lastmod = 2020-04-02T22:03:21-07:00
draft = false
+++

## 文件结构 {#文件结构}

```go
package main

import "fmt"

func main() {
    //comment
    fmt.Println("Hello, World")
}
```

1.  包名，每个程序都包含一个main包
2.  需要引入的包
3.  执行函数
4.  `//` 开头单行注释 `/*...*/` 多行注释


## 语法 {#语法}


### 变量 {#变量}

```go
var a string = "hello"

var b int

var c bool

var d = true

e := 1
```


### 常量 {#常量}

```go
const a int = 1
const (
    b = "hello"
    c = false
)
```


### 条件语句 {#条件语句}


#### if {#if}

```go
if a < 20 {
    fmt.Print("11")
}
```


#### if...else... {#if-dot-dot-dot-else-dot-dot-dot}

```go
if a < 20 {
    fmt.Print("11")
} else {
    fmt.Print("22")
}
```


#### switch {#switch}

```go
switch {
    case grade == "A" :
        fmt.Printf("优秀!\n" )
    case grade == "B", grade == "C" :
        fmt.Printf("良好\n" )
    case grade == "D" :
        fmt.Printf("及格\n" )
    case grade == "F":
        fmt.Printf("不及格\n" )
    default:
        fmt.Printf("差\n" );
}
```


#### select {#select}

```go
var c1, c2, c3 chan int
var i1, i2 int
select {
    case i1 = <-c1:
        fmt.Printf("received ", i1, " from c1\n")
    case c2 <- i2:
        fmt.Printf("sent ", i2, " to c2\n")
    case i3, ok := (<-c3):  // same as: i3, ok := <-c3
        if ok {
        fmt.Printf("received ", i3, " from c3\n")
        } else {
        fmt.Printf("c3 is closed\n")
        }
    default:
        fmt.Printf("no communication\n")
}
```


### 循环语句 {#循环语句}


#### for init; condition; post { } {#for-init-condition-post}

```go
sum := 0
for i := 0; i <= 10; i++ {
    sum += i
}
```


#### for condition { } {#for-condition}

```go
for key, value := range oldMap {
    newMap[key] = value
}
```


#### for { } {#for}

```go
sum := 0
for {
    sum++ // 无限循环下去
}
```


### 函数定义 {#函数定义}

```go
func max(a, b) int {
    var result int

    if (a > b) {
        result = a
    } else {
        result = b
    }
    return result
}

max(1,2)

//多返回值
func swap(x, y string) (string, string) {
   return y, x
}

func main() {
   a, b := swap("Google", "Runoob")
   fmt.Println(a, b)
}
```

-   方法名首字母大写的为包pulic方法
-   方法名首字母小写的为包private方法


### 数组 {#数组}

```go
var variable_name [SIZE] variable_type
var balance [10] float32
```


### 指针 {#指针}

```go
var a int= 20   /* 声明实际变量 */
var ip *int        /* 声明指针变量 */

ip = &a  /* 指针变量的存储地址 */

fmt.Printf("a 变量的地址是: %x\n", &a  )

/* 指针变量的存储地址 */
fmt.Printf("ip 变量储存的指针地址: %x\n", ip )

/* 使用指针访问值 */
fmt.Printf("*ip 变量的值: %d\n", *ip )
```


### 切片 (slice) {#切片--slice}

```go
// int类型动态数组
var arr1 []int
//另一种写法, 3是初始长度
var arr1 []int = make([]int, 3)
//简写
arr1 := make([]int, 3)
```


### Map (字典) {#map--字典}

```go
var map_variable map[key_data_type]value_data_type
map_variable := make(map[key_data_type]value_data_type)

var dict map[string]string
//简写
dict := make(map[string]string)

dict["a"] = "11111"
```


### 结构体 struct {#结构体-struct}

```go
type Person struct {
    Name string
    Age int
}

func (p *Person) SayHello() {
    fmt.Println("hello, ", p.Name)
}

func main() {
    var guy = new(Person)
    guy.name = "jirex"
    guy.SayHello()
}
```


### interface {#interface}

蓝图

```go
type Friend interface {
    SayHello()
}
```


## 命令行cli {#命令行cli}


### go run `main.go` {#go-run-main-dot-go}

执行go文件


### go build `main.go` {#go-build-main-dot-go}

生成可执行文件


### go fmt `main.go` {#go-fmt-main-dot-go}

格式化文件


## Tips {#tips}


### `{` 不能单独放一行 {#不能单独放一行}
