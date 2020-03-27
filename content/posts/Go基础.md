+++
title = "Go基础"
author = ["jirex"]
lastmod = 2020-03-27T17:59:52+08:00
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


## 命令行cli {#命令行cli}


### go run `main.go` {#go-run-main-dot-go}

执行go文件


### go build `main.go` {#go-build-main-dot-go}

生成可执行文件


### go fmt `main.go` {#go-fmt-main-dot-go}

格式化文件
