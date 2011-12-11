---
layout: post
title: "在Ubuntu 11.10下搭建Vim-Rails开发环境"
date: 2011-12-11 11:54
comments: true
categories: [Ubuntu, Rails, Ruby, VIM]
---

###1 安装先决条件
`sudo apt-get install build-essential bison openssl libreadline6
libreadline6-dev curl git-core zlib1g zlib1g-dev libssl-dev libyaml-dev
libsqlite3-0 libsqlite3-dev sqlite3 libxml2-dev libxslt-dev autoconf
libc6-dev xclip ncurses-dev automake`

###2 安装rvm

####2.1  安装
`$ bash < <(curl -s https://raw.github.com/wayneeseguin/rvm/master/binscripts/rvm-installer)`
####2.2 shell 脚本配置
`$ echo '[[ -s "$HOME/.rvm/scripts/rvm" ]] && ."$HOME/.rvm/scripts/rvm" # Load RVM function' >> ~/.profile`
####2.3 reload shell
`$ source .profile`
####2.4 验证是否安装正确
`$ type rvm | head -1`
####2.5 查看ubuntu下各类ruby版本需要哪些条件
`$ rvm requirements`
###3 安装ruby
`rvm install 1.9.2`  
编译yaml-0.1.4时出错，报缺libtool  
`sudo apt-get install libtool`

###4 安装rails
`rvm gemset create rails313`  
`rvm use 1.9.2@rails313 --default`  
`gem install rails --no-ri --no-rdoc`  

###5 配置vim
`sudo apt-get install vim-gnome`
###6 解决gvim在ubuntu 11.10中的问题
####解决gvim在Ubuntu 11.10中导致电脑很卡的问题**
运行：  
`echo 'alias gvim="gvim -f"' >> ~/.bashrc`  
`source ~/.bashrc`
####解决提示“pixmap”的问题
如果终端中提示：
(gvim:2353): Gtk-WARNING **: 无法在模块路径中找到主题引擎：“pixmap”  
解决方法是运行：  
`sudo apt-get install gtk2-engines-pixbuf`

###7 配置vim插件
`curl https://raw.github.com/SaitoWu/janus/master/bootstrap.sh -o - | sh`

感谢SaitoWu同学迁移到linux环境  
执行到最后报段错误:  
gvim报拦截到致命信号(deadly signal) SEGV  
发现是command-t和ruby 1.9.2的冲突  

安装系统自带ruby  
`sudo apt-get install ruby`  
`sudo apt-get install ruby1.8-dev`  
删除~/.vim/plugin/command-t.vim，在～/.vim/下重新rake。修复。

再次碰到错误：  
Taglist: Exuberant ctags (http://ctags.sf.net) not found in PATH. Plugin is not loaded. 
请按 ENTER 或其它命令继续  

执行：`sudo apt-get install exuberant-ctags`

###8 安装Monaco字体
下载monaco.ttf  
放入/usr/share/fonts/truetype  
`sudo fs-cache -fv`  

###9 修改.gvimrc加入字体设置
`set guifont=monaco`

###10 最终效果
{% img http://l.ruby-china.org/photo/02718827d45dec0b060e1e7b416c94e2.png %}

