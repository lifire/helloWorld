# 如何使用GitHub #
如何将本地项目上传到GitHub

## 一，登录GitHub官网注册账号 ##

   官网地址：https://github.com

## 二，创建SSH Key。用来建立本地电脑与GitHub的安全通信。 ##

打开git bash，输入以下命令：

    ssh-keygen -t rsa -C "youremail@exapmle.com"


在弹出的提示中一路回车确认就可以，顺利的话，会在用户主目录中生成.ssh目录，并有**id_rsa** 和 **id_rsa.pub**两个文件，这两个就是SSH Key的秘钥对，id_rsa 是私钥，不能泄露出去，id_rsa.pub是公钥，可以对外公开。我们需要做的就是打开id_rsa.pub，复制里边的内容。


## 三，登录GitHub，配置SSH Key ##

在右上角用户头像下拉列表中选择“settings”，然后在页面左侧，打开“SSH and GPG keys”栏目，选择“New SSH key”。title可以填入任意标题，key文本框里添加id_rsa.pub文件的内容即可。

点击“Add SSH key”，就可以看到已经添加的Key了。

为什么GitHub需要SSH Key呢？因为GitHub为所有用户免费公开仓库，所有人都能访问，但只有所有者和授权用户才有权限修改，SSH Key正是作为用户权限验证用的，确定你是否有权限对这个仓库做修改。

另外SSH Key可以创建多个，方便同个账号可以在多台电脑上往GitHub推送，在家或者出差都可以远程办公。


## 四，创建仓库 ##

1，在右上角的下拉列表中选择“your repositories”，然后new一个新仓库

2，填写你的仓库名称，然后创建

3，创建成功后，后跳到仓库的首页，因为此时仓库还是空的，会展示一个教你关联仓库的帮助文档

4，如果你本地还没有创建项目，可以在git bash执行以下操作：

        echo "# helloWorld" >> README.md    // 创建README.md文件
        git init                            // 初始化本地仓库
        git add README.md                   // 将README.md添加到缓存区
        git commit -m "first commit"        // 将缓存区的文件正式添加到仓库，并添加说明
        git remote add origin https://github.com/yourname/helloWorld.git  //将本地仓库和远程仓库联系起来
        git push -u origin master           // 将本地库的所有内容推送到远程库上

5，如果你本地上已经有创建项目了，可以直接从关联用户仓库开始

        git remote add origin https://github.com/yourname/helloWorld.git
        git push -u origin master

五，本地项目操作说明

   1，进入项目目录，启动Git bash

   2，建立本地仓库

        输入命令：git init

   3，将项目中所有文件添加到git仓库缓存区

        输入命令：git add .
		[git add name.type] 添加指定文件/文件夹
		[git rm name.type] 删除指定文件/文件夹

   4，推送到仓库并添加注释说明

        输入命令：git commit -m "注释内容"

   5，推送到GitHub远程仓库

        输入命令：git push origin master


----------


使用webpack搭建项目的时候，npm初始化的时候，会生成一个node_modules库，里边的文件非常多，因为是公用的库，我们可以不必一起上传到git远程仓库中，从而提升提交代码的效率。
那么如何推送的时候忽略调node_modules库呢？

1，在你的项目目录里，新建一个.gitignore文件

    touch .gitignore

2,打开.gitignore文件,在里面输入node_modules，保存并退出

	node_modules

这样就可以了，下次你再向GitHub推送的时候，就不会把node_modules一起推送了。