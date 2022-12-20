
---
title: Hexo建站全攻略
date: 2022-11-06 09:20:21
tags:
---
一、Hexo简介
Hexo 是一个快速、简洁且高效的博客框架，使用 Markdown解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

二、搭建流程（Linux）
1、准备工作
安装node.js
下载地址：https://nodejs.org/en
推荐下载LTS版，默认安装即可

2、安装hexo
{% codeblock %}
npm install -g hexo-cli
{% endcodeblock %}

3、初始化hexo文件夹
（1）、创建文件夹
所有的建站文件都会存储在一个文件夹中，所以挑选一个位置，创建一个文件夹，路径和文件夹名字最好是英文。
例如我在/home路径下创建myweb文件夹
（2）、初始化文件夹
{% codeblock %}
cd /home/myweb
{% endcodeblock %}

{% codeblock %}
hexo init
{% endcodeblock %}

4、安装依赖包
{% codeblock %}
npm install
{% endcodeblock %}



5、本地运行hexo
{% codeblock %}
hexo generate
{% endcodeblock %}

{% codeblock %}
hexo server
{% endcodeblock %}


完成后在浏览器中打开：http://localhost:4000






打开后如下图所示，此时hexo就运行起来了


6、创建仓库
在github上创建博客的仓库，创建仓库地址：https://github.com/new
例如我的github帐号名为w5l6j9，那么我的Repository的name就必须为文w5l6j9.github.io

7、修改配置文件
（1）、修改deploy
打开 home\myweb下的_config.yml文件，搜索deploy，修改为如下格式，其中repository就是刚才创建的仓库地址，需要注意的是每个字段后都有冒号，冒号后有一个英文的空格
修改如下所示：

deploy:
  type: git
  repository: https://github.com/w5l6j9/w5l6j9.github.io.git
  branch: master
（2）、修改URL
搜索ULR，将url替换成https://w5l6j9.github.io/

\#URL
\##If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'

url: https://w5l6j9.github.io
8、设置SSH keys
（1）、生成SHH keys
输入下面的命令，查看是否生成过ssh，如果有则将根目录下的.ssh文件夹删除
{% codeblock %}
ls -al ~/.ssh
{% endcodeblock %}

然后依次输入下面的命令，邮箱为你自己申请github的邮箱
{% codeblock %}
ssh-keygen -t rsa -C "example@qq.com"

ssh-agent -s

ssh-add ~/.ssh/id_rsa
{% endcodeblock %}


如果出现Could not open a connection to your authentication agent.则依次输入下面的指令
{% codeblock %}
eval `ssh-agent -s`

ssh-add
{% endcodeblock %}

然后输入下面的命令，复制公钥
{% codeblock %}
clip < ~/.ssh/id_rsa.pub
{% endcodeblock %}

（2）、设置SSH keys
点击github的头像，选择Settings

设置

然后依次点击左侧的SSHand GPG keys和右上角的New SSH key

添加SSH

title可以随意取名，将刚才复制的公钥粘贴到key的文本框中，点击Add SHH key，要求输入密码，输入后即可添加成功。

（3）、测试
输入
{% codeblock %}
ssh -T git@github.com
{% endcodeblock %}

会出现提示，输入yes，再次按回车，当出现下图所示的文字时，表示测试成功，SSH配置成功！

如果出现remote: Support for password authentication was removed on August 13, 2021. Please use a personal access token instead.

意思就是要用个人令牌连接

具体解决方法看这篇博客
https://blog.csdn.net/qq_42714262/article/details/119706383

最后把config.yml中的地址替换成如下的地址(账号名换成你自己的)
  repository: https://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@github.com/w5l6j9/w5l6j9.github.io


9、部署到github上
输入
{% codeblock %}
hexo generate
{% endcodeblock %}

然后再输入

{% codeblock %}
hexo deploy
{% endcodeblock %}

如果出现以下错误：

ERROR Deployer not found: github
就需要安装hexo-deployer-git模块，
输入
{% codeblock %}
npm install hexo-deployer-git --save
{% endcodeblock %}

安装好之后重新执行
{% codeblock %}
hexo deploy
{% endcodeblock %}

10、访问博客
在浏览器打开：https://w5l6j9.github.io/ ，即可访问基于hexo的博客了！
PS：部署之后可能有延迟，请耐心等待。

11、命令简化
hexo的命令可以简写，如下：

| 命令 | 简写 |
| :-------------: | :--------------: |
| hexo generate | hexo g |
| hexo deploy | hexo d |
| hexo server | hexo s |

参考:https://juemuren4449.com/archives/build-hexo-blog-guide
