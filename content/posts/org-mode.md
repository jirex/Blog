+++
title = "org-mode"
author = ["jirex"]
lastmod = 2020-03-26T09:26:34+08:00
draft = false
+++

## 语法 {#语法}


### **bold** {#bold}


### _italic_ {#italic}


### <span class="underline">underlined</span> {#}


### `code` {#code}


### `verbatim` {#verbatim}


### ~~中划线~~ {#}


### [google](https://www.google.com) {#google}

外部链接[[][]],前面是链接, 后面是文字


### <a id="org24b3aff"></a> {#}

内部链接


### `TODO` first todo {#todo-first-todo}


### 无序列表 {#无序列表}

-   xxx
-   yyy
-   zzz


### 有序列表 {#有序列表}

1.  111
2.  222
3.  333


### 子任务 <code>[0/1]</code> {#子任务}

-   [-] 大分类 <code>[1/2]</code>
    -   [X] 中分类1
    -   [-] 中分类2
        -   [X] 小分类1
        -   [ ] 小分类2


### 标签 {#标签}

-   位置：只能在各级标题的行末端, 只能在标题行
-   命名：可以包含数字、字幕、下划线或@符合

`:label1:label2:`


### 时间戳 {#时间戳}

-   `<>` 激活的时间，加入日程表
-   `[]` 非激活的时间，不加入日程表
-   `--` 连接的两个时间戳，表示时间段


### src block {#src-block}

`<s <tab>` 代码块

```sh
echo "hello world"
```


## 配置 {#配置}


### todo关键字 {#todo关键字}

```elisp
(setq org-todo-keywords
'((type "工作(w!)" "学习(s!)" "休闲(l!)" "|")
    (sequence "PENDING(p!)" "TODO(t!)"  "|" "DONE(d!)" "ABORT(a@/!)")
))
```

-   "|" 用来分割 `未完成` 和 `完成` 两种状态
-   "!" 表示时间戳，改变到该状态是插入时间戳
-   "@" 表示改变到该状态时需要填写文字说明


### 改变TODO关键字外观 {#改变todo关键字外观}

```elisp
(setq org-todo-keyword-faces
'(("PENDING" .   (:background "LightGreen" :foreground "gray" :weight bold))
    ("TODO" .      (:background "DarkOrange" :foreground "black" :weight bold))
    ("DONE" .      (:background "azure" :foreground "Darkgreen" :weight bold))
    ("ABORT" .     (:background "gray" :foreground "black"))
))
```


### 改变优先级外观 {#改变优先级外观}

```elisp
;; 优先级范围和默认任务的优先级
(setq org-highest-priority ?A)
(setq org-lowest-priority  ?E)
(setq org-default-priority ?E)
;; 优先级醒目外观
(setq org-priority-faces
'((?A . (:background "red" :foreground "white" :weight bold))
    (?B . (:background "DarkOrange" :foreground "white" :weight bold))
    (?C . (:background "yellow" :foreground "DarkGreen" :weight bold))
    (?D . (:background "DodgerBlue" :foreground "black" :weight bold))
    (?E . (:background "SkyBlue" :foreground "black" :weight bold))
))
```


### 预定义标签 {#预定义标签}

```elisp
(setq org-tag-alist '(("@work" . ?w) ("@home" . ?h) ("laptop" . ?l)))
```


## org functions {#org-functions}


## org values {#org-values}


### org-log-done {#org-log-done}

todo切换为done的时候是否需要加时间戳


### org-agenda-files {#org-agenda-files}

agenda查找TODOs和scheduled项目 是一个list


## 快捷键 {#快捷键}


### C-RET {#c-ret}

增加同级 headline


### M-S-RET {#m-s-ret}

增加同级TODO headline
在子任务中，增加子项


### C-c C-o {#c-c-c-o}

org-open-at-point 打开链接


### C-c C-t {#c-c-c-t}

循环TODO状态


### C-c / t {#c-c-t}

显示当前文件所有todo


### C-c . {#c-c-dot}

添加日期


### C-u C-c . {#c-u-c-c-dot}

添加时间和日期


### S-left/right {#s-left-right}

选择日期


### C-c C-c {#c-c-c-c}

添加tag


### C-c \* {#c-c}

将当前行转化为标题


### C-c - {#c-c}

将当前行转化为列表


### C-c C-c {#c-c-c-c}

-   子任务切换状态
-   在标题行，修改标签
-   在src块里面，执行代码块


### C-c C-q {#c-c-c-q}

更改标签


### C-c . {#c-c-dot}

插入日期，激活的


### C-c ！ {#c-c}

插入日期，非激活的


### C-c ' {#c-c}

在src块里，编辑代码块
