---
layout: post
title:  git ssh配置
date:   2018-07-06 00:00:00 +0800
categories: "技术杂论"
tag: ""
---

<p>每次提交git都要输入账号密码，今天一怒之下准备配置一下。过程如下：</p>
<p>git连接方式分为两种：<a>https</a>和<a>ssh</a>，其中https连接方式需要每次输入用户名密码，而ssh连接方式则不需要。本教程适用于初始化项目选择连接方式是https，后期需要修改为ssh连接方式。</p>
<p>嫌麻烦的小伙伴可以用ssh方式重新拉取项目，然后依次进行第二步-第三步-第四步</p>
<p class="p30"></p>

<h4>第一步：查看当前连接方式：</h4>
	$ git remote -v
<p>https连接方式:</p>
<img src="/styles/images/sshconfig/https_lianjie.jpg" />
<p>ssh连接方式:</p>
<img src="/styles/images/sshconfig/ssh_lianjie.jpg" />        
<p class="p30"></p>


<h4>第二步：查看本地是否有公钥</h4>
	$ cd ~/.ssh
	$ ls
<p>如果出现下图红框中的文件名，说明本地已有公钥，直接进行第四步</p>
<img src="/styles/images/sshconfig/rsa_pub.jpg" />
<p class="p30"></p>

<h4>第三步：生成新的公钥</h4>
<p>设置用户名和邮箱</p>
	$ git config --global user.name "your name"
	$ git config --global user.email "your email"
<p>生成公钥</p>
	$ ssh-keygen -t rsa -C "your email"
<p>按三次回车即可，生成的密码是空，如需配置密码请自行解决</p>
<p class="p30"></p>

<h4>第四步：在git上添加公钥</h4>
<p>1.复制C:\Users\[你的用户]\.ssh\id_rsa.pub中的内容</p>
<p>2.打开git设置</p>
<img src="/styles/images/sshconfig/settings_1.jpg" />
<p>3.新增ssh</p>
<img src="/styles/images/sshconfig/settings_2.jpg" />
<p>4.保存</p>
<img src="/styles/images/sshconfig/settings_3.jpg" />
<p class="p30"></p>

<h4>第五步：更换连接方式</h4>
	$ git remote rm origin
	$ git remote add origin "ssh地址：获取方法见第一步中ssh连接方式(不需要加引号)"
	$ git push -u origin "当前分支名称(不需要加引号)"
<p>设置完成，可以提交一下git看是否配置是否成功</p>
<p class="p30"></p>

<h4>注意：</h4>
<p>如果提交的时候出现以下错误信息，排除网络等原因，是因为ssh公钥不对，请删除本地公钥后从第三步重新开始</p>
	Permission denied (publickey).
	fatal: Could not read from remote repository.

	Please make sure you have the correct access rights
	and the repository exists.
<p>最后安利一个软件:<a href="http://www.voidtools.com/">everything</a>,全盘搜索文件利器。</p>


