# git

## 设置签名

签名为了区分一个项目组的代码是由哪一位成员提交的，这里的签名和github账号没有关系

签名分为两个级别：

1. 项目级别/仓库级别 git config
2. 系统用户级别 git config --global

如果两个签名都有的话，系统优先选择项目级别的签名。

案例：

```git
git config --global user.name Carlos
git config --global user.email 522929745@qq.com
```

查看项目的git配置信息

cat .git/config

得到下面内容,因为这个项目已经用了秘钥关联，所以没有[user]的信息，否则会有

```git
$ cat .git/config
[core]
        repositoryformatversion = 0
        filemode = false
        bare = false
        logallrefupdates = true
        ignorecase = true
[remote "origin"]
        url = git@gitee.com:CarlosW/vue_shop.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
        remote = origin
        merge = refs/heads/master
[branch "login"]
        remote = origin
        merge = refs/heads/login
[branch "rights"]
        remote = origin
        merge = refs/heads/rights
[branch "goods_cate"]
        remote = origin
        merge = refs/heads/goods_cate
[branch "goods_params"]
        remote = origin
        merge = refs/heads/goods_params
[branch "goods_list"]
        remote = origin
        merge = refs/heads/goods_list
```

#### 查看全局设置签名的方法

cd ~  切换到用户根目录

pwd 查看当前所在的目录

 ls -lA|less  查看该目录所有文件包括隐藏文件

cat .gitconfig  查看用户根目录设置的全局签名

#### 撤销git add(从暂存区删除文件)

工作区=家

暂存区=运输车

仓库=仓库

git rm --cached aaaa.txt

当然也可以这样

撤销git add的所有的文件

git rm --cached /*

#### vim编辑器

如果光标前面有:在闪，说明当前在vim编辑器

显示行号      :set nu

进入编辑模式    :i

退出vim   ：wq

当然git commit可以这样用：

git commit -m '信息' abc.txt



#### 查看版本：查看历史版本

多屏显示控制方式：

b向上翻页

q退出

1.git log（只显示历史的版本，不会显示未来的版本）

会出现哈希算法出来的版本下标

2.git log --pertty=oneline(简便的显示)

3.git log --oneline(简便的显示，只显示哈希值的一部分)

4.git reflog 有点像3.，但是会有提示，提示你需要移动几步指针到哪个版本，我个人感觉很好用，而且可以显示未来的版本

#### 版本前进和后退

HEAD就是指针

前进后退有三种方式

1. 基于版本下标
2. 用^  只能后退
3. 用~  只能后退



案例：

git reset --hard 下标（下标可以用上面只显示的哈希值的一部分就足够了，因为这一部分以及可以区分出不同的版本号）

git reset --hard HEAD^ 后退一个版本

git reset --hard HEAD^^^ 后退三个版本

git reset --hrad HEAD~3回退三个版本

三个移动版本的参数

1. --soft 仅仅在仓库移动指针
2. --mixed 移动仓库指针，重置运输车
3. --hard 移动仓库指针，重置运输车和家 所以这个用的最多

### git diff比较差异

如果没有加其他参数，那么git diff就是家里和运输车上进行比较

git diff HEAD 比较所有文件



### 热修复一般用hot_fix分支

git可以用tab键来进行补全要输入的内容，比较智能



#### 版本冲突

svn会产生新的文件，但是git不会

产生冲突之后，修改文件到满意之后，git add .  

然后git commit -m '提示信息' 注意这里不能加文件名



#### git pull等于

fetch+merge 也就是说第一步是先抓取，第二步是合并。如果改的内容不是很多的情况的话，会用到pull





#### ssh



GitHub网站左侧的SSH and GPG keys，然后点击页面的new ssh key。title就是你的公钥描述信息。

key就是你电脑上面的ssh

生成电脑的ssh：

cd ~ 到用户根目录

在这个目录创建一个.gitconfig

ssh-keygen -t ras -C “邮箱地址”

案例：

ssh-keygen -t ras -C "522929745@qq.com"

然后会提示你：

enter file in which to save the key (一个路径名)       提示你生成的ssh密钥会保存在哪一个文件夹下

如果此时你已经有了一个ssh密钥还会提示你 overwrite(y/n)?



然后文件夹里面会生成    

这个是私钥：id_rsa

这个是公钥：id_rsa.pub

然后我们就可以copy公钥里面的内容到GitHub上面了