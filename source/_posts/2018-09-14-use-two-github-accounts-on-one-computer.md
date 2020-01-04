---
title: 在一台电脑上使用两个Github账号
original: true
date: 2018-09-14 21:44:19
description: 最近在使用github的时候,有这样的一个需求,就是一台电脑上登录两个github账号,并上传项目和更新自己的代码,大家都知道需要给该账号添加一个SSH key才能访问，当然如果你在多台机器使用一个账户，你可以为该账户添加多个SSH key。由于github是使用SSH key的fingerprint来判定你是哪个账户，而不是通过用户名，这样你就可以在设置完之后，在本地直接执行下面的语句，它就会自动使用你的.ssh/id_rsa.pub所对应的账户进行登陆，然后执行相关命令。
categories: 经验
tags: github
---
1. 查看已有`密钥`
Mac 下输入命令`ls ~/.ssh/`，看到`id_rsa`与`id_rsa_pub`则说明已经有一对密钥。
2. 生成新的公钥，并命名为`id_rsa_work`(保证与之前密钥文件名称不同即可)
`ssh-keygen -t rsa -f ~/.ssh/id_rsa_work -C "yourmail@xxx.com"`
3. 在`.ssh`文件夹下新建`config`文件并编辑(`touch config`可以创建一个config的文件)，另不同`Host`实际映射到同一`HostName`，但密钥文件不同。`Host`前缀可自定义，例子中`work`
``` bash                
Host github.com
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa

Host work.github.com
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa_work
```
<!-- more -->
4. 将生成的`id_rsa.pub`、`id_rsa_work.pub`内容复制到到对应的 repo
参考教程: [使用SSH密钥连接Github【图文教程】](http://www.xuanfengge.com/using-ssh-key-link-github-photo-tour.html)
5. 测试 ssh 链接
``` bash
$ ssh -T git@work.github.com
$ ssh -T git@github.com
#提示：Hi IEIT! You've successfully authenticated, but GitHub does not provide shell access.出现上边这句，表示链接成功
```
6. 现在开始使用新的公私钥进行工作吧
    - 情况一：将项目`clone`到本地， `folder-name`是本地文件夹路径
    ``` bash
    $ git clone git@work.github.com:xxx(用户名)/xxx(项目名).git folder-name
    ```
    - 情况二：
    ``` bash
    $ echo "# bbb" >> README.md
    $ git init
    $ git add README.md
    $ git commit -m "first commit"
    $ git remote add origin git@work.github.com:ijcad/bbb.git
    $ git push -u origin master
    ```
    - 情况三：
    ``` bash
    $ git clone git@github.com:xxx/xxx.git folder-name #原项目地址
    $ git remote rm origin
    $ git remote add origin git@work.github.com:XXX/XXX.git #重新链接新的远程仓库
    $ git remote -v #查看远程仓库有没有成功
    ```
7. 进入`folder-name`项目目录。单独设置取消全局用户名/邮箱设置
    - 第一步：取消全局`用户名`/`邮箱`配置
    ``` bash
    $ git config --global --unset user.name #取消全局用户名
    $ git config --global --unset user.email #取消全局邮箱
    ```
    - 第二步：单独设置每个repo`用户名`/`邮箱`配置
    ```bash
    $ git config user.name "xxxx" #单独设置用户名
    $ git config user.email "xxxx@xx.com" #单独设置邮箱   
    ```
8. 添加`README.md`文件修改完后保存。完成。
``` bash
$ echo "# bbb" >> README.md
$ git add README.md
$ git commit -m "update README.md"
$ git push -u origin master
```