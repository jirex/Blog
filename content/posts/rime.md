+++
title = "Rime输入法"
author = ["jirex"]
lastmod = 2020-04-10T15:32:12+08:00
draft = false
+++

## 配置文件要求 {#配置文件要求}

-   UTF-8编码
-   建议用UNIX换行符 (LF)
-   第一行为注释，防止BOM头影响

<!--listend-->

```yaml
# RIME default setting

```


## 文件及作用 {#文件及作用}


### 共享文件夹 {#共享文件夹}

`"/Library/Input Methods/Squirrel.app/Contents/SharedSupport/"`


### 用户文件夹 {#用户文件夹}

`~/Library/Rime/`

-   `default.yaml` 全局设定
-   `weasel.yaml` 发行版设定
-   `<方案标识>.schema.yaml` 预设输入方案副本
-   `installation.yaml` 安装信息
-   `user.yaml` 用户状态信息
-   `<方案标识>.prism.bin` Rime棱镜
-   `<词典名>.table.bin` Rime固态词典
-   `<词典名>.reverse.bin` Rime反查词典
-   `<词典名>.userdb.kct` 用户词典
-   `<词典名>.userdb.txt` 用户词典快照
-   `default.custom.yaml` 用户全局设定的定制信息
-   `<方案标识>.custom.yaml` 用户对预设输入方案的定制信息


## 方案定义 schema.yaml {#方案定义-schema-dot-yaml}

-   描述

<!--listend-->

```yaml
# 以下代碼片段節選自 luna_pinyin.schema.yaml

schema:
  schema_id: luna_pinyin
  name: 朙月拼音
  version: "0.9"
  author:
    - 佛振 <chen.sst@gmail.com>
  description: |
    Rime 預設的拼音輸入方案。
```

-   开关
    -   `ascii_mode` 中英文转换开关
    -   `full_shape` 全角/半角符号开关
    -   `extended_charset` 字符集开关
    -   `simplification` 简/繁转化字开关

<!--listend-->

```yaml
switches:
  - name: ascii_mode
    reset: 0
    states: ["中文", "西文"]
  - name: full_shape
    states: ["半角", "全角"]
  - name: extended_charset
    states: ["通用", "增廣"]
  - name: simplification
    states: ["漢字", "汉字"]
  - name: ascii_punct
    states: ["句讀", "符號"]
```
