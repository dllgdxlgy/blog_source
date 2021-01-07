---
title: mac安装brew

date: 2020-10-15 14:33:20
tags:
- 软件
- Mac
categories:
- 搭建
---

<center>一人为轴，一人悬空～</center>

<!-- more -->

mac上执行

```js
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

就完美解决～

以下是我的安装过程～



```js
Last login: Thu Oct 15 14:17:49 on ttys000
LGYdeMacBook-Pro:~ lvguangyue$ brew search wget
-bash: brew: command not found
LGYdeMacBook-Pro:~ lvguangyue$ ruby -e “$（curl -fsSL /homebrew/go“
ruby: invalid option -f  (-h will show valid options) (RuntimeError)
LGYdeMacBook-Pro:~ lvguangyue$ /bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"

              开始执行Brew自动安装程序
             [cunkai.wang@foxmail.com]
           [2020-10-15 14:22:57][10.13]
       https://zhuanlan.zhihu.com/p/111014448


请选择一个下载镜像，例如中科大，输入1回车。
源有时候不稳定，如果git克隆报错重新运行脚本选择源。cask非必须，有部分人需要。
1、中科大下载源 2、清华大学下载源 3、北京外国语大学下载源 4、腾讯下载源（不显示下载进度） 5、阿里巴巴下载源(缺少cask源)
请输入序号: 1

  你选择了中国科学技术大学下载源

！！！此脚本将要删除之前的brew(包括它下载的软件)，请自行备份。
->是否现在开始执行脚本（N/Y）y

--> 脚本开始执行
==> 通过命令删除之前的brew、创建一个新的Homebrew文件夹
(设置开机密码：在左上角苹果图标->系统偏好设置->"用户与群组"->更改密码)
(如果提示This incident will be reported. 在"用户与群组"中查看是否管理员)
请输入开机密码，输入过程不显示，输入完后回车
Password:
开始执行
-> 创建文件夹 /usr/local/Homebrew
此步骤成功
-> 创建文件夹 /usr/local/Caskroom
此步骤成功
-> 创建文件夹 /usr/local/Cellar
此步骤成功
-> 创建文件夹 /usr/local/var/homebrew
此步骤成功
-> 创建文件夹 /usr/local/etc
此步骤成功
-> 创建文件夹 /usr/local/sbin
此步骤成功
-> 创建文件夹 /usr/local/opt
此步骤成功
-> 创建文件夹 /usr/local/share/zsh
此步骤成功
-> 创建文件夹 /usr/local/share/zsh/site-functions
此步骤成功
-> 创建文件夹 /usr/local/var/homebrew/linked
此步骤成功
-> 创建文件夹 /usr/local/Frameworks
此步骤成功
git version 2.23.0

下载速度觉得慢可以ctrl+c或control+c重新运行脚本选择下载源
==> 克隆Homebrew基本文件(32M+)

未发现Git代理（属于正常状态）
Cloning into '/usr/local/Homebrew'...
remote: Enumerating objects: 164328, done.
remote: Total 164328 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (164328/164328), 40.57 MiB | 2.42 MiB/s, done.
Resolving deltas: 100% (122161/122161), done.
此步骤成功
==> 创建brew的替身
此步骤成功
==> 克隆Homebrew Core(224M+) 
此处如果显示Password表示需要再次输入开机密码，输入完后回车
Cloning into '/usr/local/Homebrew/Library/Taps/homebrew/homebrew-core'...
remote: Enumerating objects: 806194, done.
remote: Total 806194 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (806194/806194), 320.67 MiB | 2.25 MiB/s, done.
Resolving deltas: 100% (541877/541877), done.
Updating files: 100% (5552/5552), done.
此步骤成功
==> 克隆Homebrew Cask(248M+) 类似AppStore 
此处如果显示Password表示需要再次输入开机密码，输入完后回车
Cloning into '/usr/local/Homebrew/Library/Taps/homebrew/homebrew-cask'...
remote: Enumerating objects: 485405, done.
remote: Total 485405 (delta 0), reused 0 (delta 0)B | 2.42 MiB/s
Receiving objects: 100% (485405/485405), 220.07 MiB | 2.23 MiB/s, done.
Resolving deltas: 100% (345258/345258), done.
此步骤成功
==> 配置国内镜像源HOMEBREW BOTTLE
此步骤成功

==> 安装完成，brew版本

检测到你不是最新系统，会有一些报错，请稍等Ruby下载安装;
    
brew -v

==> Downloading https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles/bottles-portable-ruby/portable-ruby-2.6.3_2.yosemite.bottle.tar.gz
######################################################################## 100.0%
==> Pouring portable-ruby-2.6.3_2.yosemite.bottle.tar.gz
Homebrew 2.5.6-41-g8aa6502-dirty
Homebrew/homebrew-core (git revision a7549a; last commit 2020-10-15)
Homebrew/homebrew-cask (git revision 499c7; last commit 2020-10-15)
Brew前期配置成功

==> brew update

==> Homebrew has enabled anonymous aggregate formula and cask analytics.
Read the analytics documentation (and how to opt-out) here:
  https://docs.brew.sh/Analytics
No analytics have been recorded yet (or will be during this `brew` run).

==> Homebrew is run entirely by unpaid volunteers. Please consider donating:
  https://github.com/Homebrew/brew#donations
Already up-to-date.

        上一句如果提示Already up-to-date表示成功
            Brew自动安装程序运行完成
              国内地址已经配置完成

                初步介绍几个brew命令

        本地软件库列表：brew ls
        查找软件：brew search google（其中google替换为要查找的软件关键字）
        查看brew版本：brew -v  更新brew版本：brew update

现在可以输入命令open ~/.zshrc -e 或者 open ~/.bash_profile -e 整理一下重复的语句(运行 echo $SHELL 可以查看应该打开那一个文件修改)

        https://zhuanlan.zhihu.com/p/111014448  欢迎来给点个赞
```

