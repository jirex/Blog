+++
title = "Git两种走代理方式"
author = ["jirex"]
lastmod = 2020-03-25T17:11:23+08:00
tags = ["git"]
draft = false
+++

## HTTP形式 {#http形式}

`git clone https://github/owner/repo.git`

```bash
#设置
git config --global http.proxy "socks5://127.0.0.1:1080"
git config --global https.proxy "socks5://127.0.0.1:1080"
#取消
git config --global --unset http.proxy
git config --global --unset https.proxy
```


## SSH形式 {#ssh形式}

`git clone git@github.com:owner/repo.git`

```bash
#修改 ~/.ssh/config 文件（不存在则新建）：~
Host github.com #多ssh key时，可设别名
   HostName github.com
   User git
   # 走 HTTP 代理
   ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=8080
   # 走 socks5 代理（如 Shadowsocks）
   ProxyCommand nc -v -x 127.0.0.1:1080 %h %p
```
