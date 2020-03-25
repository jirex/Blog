+++
title = "Git两种走代理方式"
author = ["jirex"]
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
修改 ~/.ssh/config 文件（不存在则新建）：

```bash
# 必须是 github.com
Host github.com
   HostName github.com
   User git
   # 走 HTTP 代理
   ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=8080
   # 走 socks5 代理（如 Shadowsocks）
   ProxyCommand nc -v -x 127.0.0.1:1080 %h %p
```
