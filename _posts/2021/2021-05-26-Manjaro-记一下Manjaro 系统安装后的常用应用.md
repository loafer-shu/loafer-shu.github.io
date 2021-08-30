---
layout: post
title: Manjaro 常用应用
date: 2021-05-26 15:51:40 +08:00
categories: [Linux,Manjaro]
---

## 记录一下安装Manjaro后安装的软件

内容大多收集于自己安装折腾过程中搜索到的文章博客。当时没全记录地址，很多内容是根据记忆来写的

### yay

```shell
sudo pacman -S yay
```

----

### zsh

自带的bash不好用，命令提示很僵硬，所以安装zsh.

#### 1. 先安装 zsh

```shell
yay -S zsh
```

再 ``which zsh`` 查看 zsh 的安装目录，比如 ``/usr/bin/zsh`` 。

接着使用 ``  chsh  `` 命令切换 shell 程序。

```shell
chsh -s /usr/bin/zsh
```

现在重启命令行就切换过来了，若没有就重启下系统。

#### 2. 再安装大佬开源的配置 oh-my-zsh

由于github不稳定，所以使用gitee的镜像安装

- 后来发现github也有镜像地址 `https://github.com.cnpmjs.org`

```shell
REMOTE=https://gitee.com/mirrors/oh-my-zsh.git sh -c "$(curl -fsSL https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh)"
```

- 升级的命令为 `upgrade_oh_my_zsh`

#### 3. 更改zsh主题

可以使用vim修改，我用自带的kate编辑。

编辑 ``~/.zshrc`` , 编辑 ``  ZSH_THEME`` 属性的值为 ``agnoster`` 。

4. **安装插件**

```shell
cd ~/.oh-my-zsh/custom/plugins
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
# 指令自动补全提示
git clone https://github.com/zsh-users/zsh-autosuggestions.git
# npm 指令提示
git clone https://github.com/lukechilds/zsh-better-npm-completion
```

然后编辑 ``~/.zshrc`` 文件

找到 ``plugins=(git)`` ，在括号中加入刚刚拉下来的插件，并在后面加入两个文件的全路径

```sh
plugins=(
 git
 wd
 zsh-syntax-highlighting
 zsh-autosuggestions
 zsh-better-npm-completion
)
source /home/real/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source /home/real/.oh-my-zsh/custom/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
source /home/real/.oh-my-zsh/custom/plugins/zsh-better-npm-completion/zsh-better-npm-completion.plugin.zsh
```

然后保存，执行 ``source ~/.zshrc`` 就ok！

----

### 中文输入法

[原文](https://manateelazycat.github.io/linux/2020/06/19/fcitx5-is-awesome.html)

```shell
sudo pacman -S fcitx5-chinese-addons fcitx5-gtk fcitx5-qt fcitx5-pinyin-zhwiki fcitx5-configtool kcm-fcitx5
```

把下面内容粘贴到 ``~/.pam_environment`` 文件中

```
GTK_IM_MODULE=fcitx5
XMODIFIERS=@im=fcitx5
QT_IM_MODULE=fcitx5
```

粘贴  `fcitx5 &` 到 `~/.xprofile` 文件中

再重启系统

----

### Java

```shell
yay -S jdk8
```

----

### Maven

点击[这里](https://archive.apache.org/dist/maven/maven-3/)去下载页面，解压放到 `/opt` 目录下

### NVM

```shell
yay -S nvm
```

----

### 将指定目录加入环境变量

我的环境变量加入的内容参考：

```shell
# ~/.bashrc 最后加入要加入的内容source /usr/share/nvm/init-nvm.shexport PUB_HOSTED_URL=https://pub.flutter-io.cnexport FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cnexport ANDROID_HOME=/home/real/Android/Sdkexport PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
```



----

### Qv2ray

```shell
sudo pacman -Syy qv2ray
```

但是我安装了打不开，不清楚原因，最终选择了到github等待[下载AppImage](https://github.com/Qv2ray/Qv2ray/releases)文件

----

### 微信

两个版本，

首先 ``wechat-uos`` ，这个版本的微信没有公众号，界面更纯粹

直接 ``yay -S wechat-uos``  即可

另外的 deepin-wine 版的微信则是win版的微信利用 wine 运行起来的

这个版本我目前是输入中文，显示有问题，不影响发送后，只是在输入框中显示为 “口” ，解决办法是，启动微信并登入后，先点开表情选择框，选择一个表情，然后再输入中文就能正常显示，每次都需要先这样操作才行，如果先输入了字，则需要重启微信再来一次上述操作。。。不清楚原因

```shell
yay -S deepin-wine-wechat# 因为我的笔记本是高分屏，所以还需要修改dpi，执行指令后在显示标签下修改即可env WINEPREFIX="/home/real/.deepinwine/Deepin-WeChat" deepin-wine5 winecfg
```



----

### QQ

TIM版就好 ``yay -S deepin.com.qq.office``

可能需要修改 `/opt/deepinwine/tools/run.sh` 文件中关于 `WINE_CMD` 的内容

我目前的值是 `WINE_CMD="deepin-wine"`

----

### QQ音乐

现在官方已经出了Linux版

点击[这里](https://y.qq.com/download/download.html)去下载就可以

AppImage版可以直接使用，deb包需要工具安装

```shell
yay -S debtap# 检查是否安装过sudo pacman -Q debtap# 若安装过执行下升级sudo debtap -u# 然后到deb包目录下sudo debtap xxx.deb# 会提示输入包名以及license，包名随便，license就GPL吧# 然后会生成x.tar.xz文件， pacman安装就可以了sudo pacman -U x.tar.xz
```

----

### 网易云音乐

```shell
yay -S netease-cloud-music
```

----


