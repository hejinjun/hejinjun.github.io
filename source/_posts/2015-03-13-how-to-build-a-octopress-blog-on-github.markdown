---
layout: post
title: "在Github上构建Octopress博客（Windows版）"
date: 2015-03-13 11:28:08 +0800
comments: true
categories: 
---
##0.写在前面的废话

昨日在看国外某大神博客的时候，看到的一篇文章就是写作者为何从Wordprss转到Octopress。第一次听说Octopress,本来没多大兴趣，以为又是一个类似Wordpress或者是Ghost这样一个平台。文章看到后面发现这东西居然可以托管在Github上，之前在搜一些文章的时候总是能看到***.github.io的域名，也曾好奇是怎么实现的，于是趁着下午的时间研究了一下。由于Git使用的不熟练，部署的过程遇到一些麻烦，幸好都能通过Google解决，废话少说，接下来就该开始Octopress探索之旅了！

##1. 在你开始之前，需要准备的几样东西
		1.请确保Git已经正确安装
		2.请确保Ruby(http://rubyinstaller.org/downloads/)已经正确安装,版本需要1.9.3以上版。
		检查方法就是命令行输入ruby --version
		3.下载Ruby Development Kit(https://github.com/oneclick/rubyinstaller/downloads/),
			解压后命令行进入解压目录执行：
			ruby dk.rb init
			ruby dk.rb install
		4.没安装过Nodejs的机器可能需要安装ExecJS（https://github.com/sstephenson/execjs），
		ExecJS可以使我们在Ruby中执行JavaScript代码。安装步骤为：gem install execjs。安装了Nodejs的机器可以略过了。

##2.本地准备

1.拷贝代码

		1. git clone git://github.com/imathis/octopress.git octopress
		2. cd octopress

2.依赖安装

		1. gem install bundler
		此步很容易报错，主要是因为墙的原因，解决方法请参考
		（http://github.kimziv.com/2013/07/19/how-to-install-ruby-gems-in-china/）：
			1. gem sources --remove https://rubygems.org/
			2. gem sources -a http://ruby.taobao.org/
			3. gem sources -l
				*** CURRENT SOURCES ***

				http://ruby.taobao.org
				# 请确保只有 ruby.taobao.org

		2. bundle install（在执行命令之前，打开octopress/Gemfile,将source "https://rubygems.org/"改为
			source "https://ruby.taobao.org"）

3.安装默认主题
	
		1. rake install

##3. Git配置

1.创建新库
	
		此步骤需要在Github上创建一个代码库，命名格式为username.github.io.
		username是Github的用户名或者是组织名

2.Octopress配置
	
		rake setup_github_pages

		此rake任务将要求你输入Github代码库的地址。复制SSH或者HTTPS地址填入即可
		git@github.com:username/username.github.io.git

3.生成发布模板
	
		1. rake generate
		2. rake deploy

		这将生成博客的发布文件，生成的文件会复制到_deploy/，将它们添加到git，并提交和推送到主分支。
		观察自己的master目录，查看是否已经与_deploy/目录相一致。如果Master目录空空荡荡则说明没有成功。
		如果出现：Updates were rejected because the tip of your current branch is behind
		请进入_deploy目录，执行git pull origin master。然后重试生成和发布步骤。

4.提交source目录
		
		1. git add .
		2. git commit -m '提交的备注信息'
		3. git push origin source

5.打开浏览器查看是否能正常运行

		
		
	