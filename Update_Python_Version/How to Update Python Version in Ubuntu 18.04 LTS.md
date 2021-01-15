```
System Version：Ubuntu 18.04 LTS
Platform：Google Cloud
Old Python Version：3.6.9
New Python Version：3.8
```

### 遇到的问题

![image-20210115184246933](https://gitee.com/inimpasse/pictures/raw/master/2021/image-20210115184246933.png)

安装MHCflurry，在脚本安装过程中Tensorflow组件时报错，在网上查找后发现可能是Tensorflow不支持该Python版本的原因，于是决定对Python版本进行升级。

### 前言

Ubuntu 18.04 LTS默认安装的是Python3.6.9，想要升级Python版本，一开始想到的解决方案是卸载自带的Python环境，再重新安装新的，这种方案可以尽量避免旧版本环境带来的干扰。但是在查找相关资料后发现，采用这种方案升级版本可能会导致系统无法启动的风险。

方案二是从Python的源代码开始安装，删除系统默认的软链命令。但是这种方法较为复杂，有可能遇到较多未知因素。

在之后的查找中，偶然看到‘[How to Install Python 3.6.1 in Ubuntu 16.04 LTS](https://ubuntuhandbook.org/index.php/2017/07/install-python-3-6-1-in-ubuntu-16-04-lts/)’这个帖子，于是就照猫画虎地按照其中的教程进行Python版本的升级，事实证明，这个方案是最简洁且有效的。

### 教程

1.打开终端，运行以下命令添加PPA(Personal Package Archive 个人包档案)

```shell
sudo add-apt-repository ppa:jonathonf/python-3.8
```

![image-20210115211318201](https://gitee.com/inimpasse/pictures/raw/master/2021/image-20210115211318201.png)

- [add-apt-repository](http://manpages.ubuntu.com/manpages/trusty/man1/add-apt-repository.1.html):增加apt仓库的命令()
- 可通过：[获取UbuntuPPA源](https://launchpad.net/)(all 44229 projects)

2.检查`apt-get`更新，通过软链命令安装Python3.8

```shell
sudo apt-get update

sudo apt-get install python3.8
```

![image-20210115211556779](https://gitee.com/inimpasse/pictures/raw/master/2021/image-20210115211556779.png)

3.要使执行`python3`使用Pyhon3.8而不是默认的3.6版本，需要执行下列指令，更换系统默认的软链命令

```shell
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1

sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.8 2
```

![image-20210115212745699](https://gitee.com/inimpasse/pictures/raw/master/2021/image-20210115212745699.png)

- [update-alternatives](https://www.jianshu.com/p/08d08713f0d1):软件版本管理命令
- 最后的数字指的是优先级

4.Python版本的切换

```shell
sudo update-alternatives --config python3
```

![image-20210115213544116](https://gitee.com/inimpasse/pictures/raw/master/2021/image-20210115213544116.png)

输入数字，可以选择使用第几个版本

### 还需要注意的

升级好Python版本后，需要升级`pip`命令版本，否则安装时也还会报错

```shell
python3 -m pip install --upgrade pip
```

![image-20210115213843551](https://gitee.com/inimpasse/pictures/raw/master/2021/image-20210115213843551.png)

升级pip版本前

![image-20210115214042217](https://gitee.com/inimpasse/pictures/raw/master/2021/image-20210115214042217.png)

![image-20210115214132023](https://gitee.com/inimpasse/pictures/raw/master/2021/image-20210115214132023.png)

升级pip版本后

### 参考资料

> 1. https://ubuntuhandbook.org/index.php/2017/07/install-python-3-6-1-in-ubuntu-16-04-lts/
> 2. https://blog.csdn.net/chaiyu2002/article/details/82698376
> 3. https://blog.csdn.net/menciushometown/article/details/77688728

