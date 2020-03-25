+++
title = "spacemacs项目解析"
author = ["jirex"]
lastmod = 2020-03-25T17:21:32+08:00
draft = false
+++

## 文件读取顺序 {#文件读取顺序}


### early-init.el {#early-init-dot-el}

emacs27专用


### init.el {#init-dot-el}


### core/core-versions.el {#core-core-versions-dot-el}

spacemacs版本号设置


### core/core-load-paths.el {#core-core-load-paths-dot-el}

-   load文件方法
-   各种文件夹全局变量


### subr-x.el {#subr-x-dot-el}

string增强


### core/core-dotspacemacs.el {#core-core-dotspacemacs-dot-el}

自定义配置核心文件

-   `SPACEMACSDIR` 环境变量为自定义路径第一选择
-   第二选择为用户home目录下 `.spacemacs.d`


### core/libs/load-env-vars.el {#core-libs-load-env-vars-dot-el}

读取环境变量库


### core/core-env.el {#core-core-env-dot-el}

环境变量核心文件


### core/libs/page-break-lines.el {#core-libs-page-break-lines-dot-el}

换页库


### core/core-hooks.el {#core-core-hooks-dot-el}

hooks方法库


### core/core-debug.el {#core-core-debug-dot-el}

debug方法库


### core/core-command-line.el {#core-core-command-line-dot-el}

命令行方法库


### core/core-funcs.el {#core-core-funcs-dot-el}

方法库


### core/core-progress-bar.el {#core-core-progress-bar-dot-el}

启动进度条库


### core/core-spacemacs-buffer.el {#core-core-spacemacs-buffer-dot-el}

home spacemacs buffer方法库


### core/core-configuration-layer.el {#core-core-configuration-layer-dot-el}

layer核心方法库


### core/core-custom-file.el {#core-core-custom-file-dot-el}

custom file方法库


### core/core-release-management.el {#core-core-release-management-dot-el}

更新spacemacs方法库


### core/core-jump.el {#core-core-jump-dot-el}

跳转定义等方法库


### core/core-display-init.el {#core-core-display-init-dot-el}

??


### core/core-themes-support.el {#core-core-themes-support-dot-el}

主题方法库


### core/core-fonts-support.el {#core-core-fonts-support-dot-el}

字体设置


### core/core-keybindings.el {#core-core-keybindings-dot-el}

按键映射库


### core/core-toggle.el {#core-core-toggle-dot-el}

toggle方法库


### core/core-micro-state.el {#core-core-micro-state-dot-el}

micro-state方法库


### core/core-transient-state.el {#core-core-transient-state-dot-el}

transient-state方法库


### core/core-use-package-ext.el {#core-core-use-package-ext-dot-el}

use-package增强


### core/core-spacemacs.el {#core-core-spacemacs-dot-el}

spacemacs加载入口方法


## 方法执行 {#方法执行}


### spacemacs/init {#spacemacs-init}

1.  是否开启debug
2.  设置advice默认接受
3.  隐藏mode-line
4.  remove gui elements (tool bar...)
5.  设置ido-mode垂直显示
6.  设置coding utf-8


### dotspacemacs/load-file {#dotspacemacs-load-file}

1.  dotspacemacs/location
2.  dotspacemacs/load-file, 加载 `.spacemacs.el` 或者 `.spacemacs.d/init.el`


### dotspacemacs/init {#dotspacemacs-init}

自定义init.el里面设置spacemacs参数


### 调整frame,是否需要decorated frame {#调整frame-是否需要decorated-frame}


### 是否全屏 {#是否全屏}


### 如果不是dump模式，dotspacemacs/user-init {#如果不是dump模式-dotspacemacs-user-init}

设置仓库地址等


### spacemacs/initialize-custom-file {#spacemacs-initialize-custom-file}

加载custom file


### 设置 dotspacemacs-editing-style {#设置-dotspacemacs-editing-style}

edit style : vim


### configuration-layer/initialize {#configuration-layer-initialize}

layer加载


### 设置获取package timeout {#设置获取package-timeout}


### 设置elpa地址 {#设置elpa地址}


### 初始化elpa packages库 {#初始化elpa-packages库}


### 确保org是elpa的，而不是内置的，如果没有，就下载 {#确保org是elpa的-而不是内置的-如果没有-就下载}


### 设置frame title {#设置frame-title}


### 加载默认主题 {#加载默认主题}


### 如果是gui emacs，加载字体 {#如果是gui-emacs-加载字体}


### 阻止emacs默认启动页面 {#阻止emacs默认启动页面}


### 加载spaecemacs buffer {#加载spaecemacs-buffer}


### 如果不是gui，重新生成一次spacemacs buffer {#如果不是gui-重新生成一次spacemacs-buffer}


### 加载环境变量 {#加载环境变量}


### 如果没有.spacemacs就生成一个 {#如果没有-dot-spacemacs就生成一个}


### configuration-layer/stable-elpa-init {#configuration-layer-stable-elpa-init}

init stable elpa


### configuration-layer/load {#configuration-layer-load}

加载layer


### run hook `configuration-layer-pre-load-hook` {#run-hook-configuration-layer-pre-load-hook}


### 个人dotfile里面的theme都下载package {#个人dotfile里面的theme都下载package}


### 读取上次保存的layers列表 {#读取上次保存的layers列表}


### 调用dotspacemacs/layers方法 {#调用dotspacemacs-layers方法}


### 判断两个layers列表是否有改变 {#判断两个layers列表是否有改变}


### save当前layers到文件夹中 {#save当前layers到文件夹中}


### configuration-layer//load {#configuration-layer-load}

真正加载layers


### configuration-layer/discover-layers {#configuration-layer-discover-layers}

查找layers


### configuration-layer//declare-used-layers {#configuration-layer-declare-used-layers}

已经使用的layers


### configuration-layer//declare-used-packages {#configuration-layer-declare-used-packages}

已经使用的packages


### 加载每个layers下的 `funcs.el` {#加载每个layers下的-funcs-dot-el}


### configuration-layer//configure-layers {#configuration-layer-configure-layers}

加载每个layers下的 `config.el`


### 如果官方layers文件夹下有 `auto-layer.el`, 加载他 {#如果官方layers文件夹下有-auto-layer-dot-el-加载他}


### 检查没有安装的包, 不是lazy install包 {#检查没有安装的包-不是lazy-install包}


### configuration-layer//install-packages {#configuration-layer-install-packages}

安装包


### configuration-layer/delete-orphan-packages {#configuration-layer-delete-orphan-packages}

删除无用的包


### spacemacs-buffer/display-startup-note {#spacemacs-buffer-display-startup-note}

启动备注


### spacemacs/setup-startup-hook {#spacemacs-setup-startup-hook}

设置启动hook


### 设置第一页面为spacemacs buffer {#设置第一页面为spacemacs-buffer}


### 开启winner-mode {#开启winner-mode}


### 调用user-config方法 {#调用user-config方法}


### 调用custom setting {#调用custom-setting}


### run-hooks 'spacemacs-post-user-config-hook {#run-hooks-spacemacs-post-user-config-hook}


### 加载用户主题 {#加载用户主题}


### 加载启动耗时 {#加载启动耗时}


### spacemacs-buffer//startup-hook {#spacemacs-buffer-startup-hook}

buffer启动hook


### dump时加载延时方法 {#dump时加载延时方法}


### 启动完成 {#启动完成}
