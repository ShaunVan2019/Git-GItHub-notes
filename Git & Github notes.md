### GIT版本控制系统

> 版本控制系统：
>
> 1.记录历史版本信息（记录每一次修改的记录）
>
> 2.方便团队相互之间协作开发
>
> .......
>
> 
>
> 常用的版本控制系统：
>
> - cvs / svn ：集中式版本控制系统
> - git ：分布式版本控制系统



#### GIT工作原理

- 工作区：我们能看到的，并且用来写代码的区域
- 暂存区：临时存储用的
- 历史区：生成历史版本

工作流程：工作区——(`$ git add -A`)——暂存区——(`$ git commit -m''`)——历史区

——(`$ git pull origin master` / `$ git push origin master`)——中央仓库

工作原理：从工作区提交到暂存区，从暂存区提交到历史区：是把内容复制一份传过去的，本区域中依然存在这些信息（只有这样才能对比出哪些文件在某个区）

代码回滚：从历史区加载回工作区 `$ git check`



**1. GIT全局配置**

> 第一次安装完成git后，我，们在全局环境下配置基本信息：我是谁？

```shell
$ git config -l  查看配置信息
$ git config --global -l  查看全局配置信息

配置全局信息：用户名和邮箱
$ git config --global user.name 'xxx'
$ git config --global user.email 'xxx@xx.xx'
```

**2. 创建仓库完成版本控制**

> 创建本地git仓库

```shell
$ git init
//=>会生成一个隐藏文件夹“.git”（这个文件夹千万不要删，因为暂存区和历史区还有一些其它的信息都在这里，删了就不是一个完整的git仓库）
```

> 在本地编写完成代码后（在工作区），把一些文件提交到暂存区

```shell
$ git add xxx  把某一个文件或者文件提交到暂存区
$ git add .  把当前仓库中所有最新修改的文件都提交到暂存区
$ git add -A  把当前仓库中所有最新修改的文件都提交到暂存区

$ git status 查看当前文件的状态（红色代表在工作区，绿色代表在暂存区，看不见东西证明所以修改的信息都已经提交到历史区）
```

> 把暂存区内容提交到历史区

```shell
$ git commit -m'描述信息：本次提交内容的一个描述'  提交到历史区

$ git log  查看历史版本信息（历史记录）
$ git reflog  包含回滚信息
```



### GIT和GIT-HUB

> GIT-HUB: https://www.github.com
>
> 
>
> 一个网站（一个开源的源代码管理平台），用户注册后，可以在自己的账户下创建仓库，用来管理项目的源代码（源代码是基于git传到仓库中）。
>
> 
>
> 我们所熟知的插件、类库、框架等都在这个平台上有托管，可以下载观看和研究源码等。

1. Settings用户设置
   - Profile 修改个人信息
   - Account 修改用户名
   - Security 修改密码
   - Emails 修改邮箱
   - ...

2. 创建仓库

   new repository

   - Settings -> Collaborators 设置协作开发的人员
   - Code 可以查看历史版本信息和分支信息

3. 把本地仓库信息提交到远程仓库

   ```shell
   //建立本地仓库和远程仓库的链接
   查看本地仓库和哪些远程仓库保持链接
   $ git remote -v
   让本地仓库和远程仓库新建一个链接  origin是随便起的一个链接名（可以改成自己想要的，只不过一般都用这个名字）
   $ git remote add origin [GIT远程仓库地址]
   删除
   $ git remote rm origin
   ```

   ```shell
   提交之前最好先拉取
   $ git pull origin master
   把本地代码提交到远程仓库（需要输入github用户名和密码）
   $ git push origin master
   ```

   ```shell
   $ git clone [远程仓库git地址] [别名：可以不设置，默认是仓库名]
   /*
    * 真实项目开发流程
    * 	 1.组长或者负责人先创建中央仓库（增加协作者）
    *   2.小组成员基于 $ git clone 把远程仓库及默认的内容克隆到本地一份
    *     解决了三件事：初始化一个本地仓库“git init”、和对应的远程仓库也保持了关联“git 
    * 	   remote add“、把远程仓库默认内容拉取到本地“git pull”
    *   3.每个组员完成自己的程序后，基于“git add/git commit”把自己修改的内容存放到历史区,
    *     然后通过“git pull/git push”把本地信息和远程仓库信息保持同步即可（可能涉及冲突的处
    *     理）
    */
   ```

   

   **git push后出现错误 ![rejected] master -> master(non-fast-forward) error:failed to push some refs to 'XXX' **

   https://www.cnblogs.com/mei1234/p/11890072.html

   #### GIT删除本地仓库

   https://blog.csdn.net/weixin_42956047/article/details/89469287

   **删除仓库，就是需要删除仓库文件夹下隐藏的 .git 文件夹！！！**

   进入项目所在目录，打开git bash，开始删除本地仓库：

   1. 显示所有本地分支（初始化时只有一个master分支）

      ```shell
      $ git branch
      ```

   2. 初始化本地版本库（重新初始化一次，可以忽略）

      ```shell
      $ git init
      ```

   3. 找到目录下隐藏的 .git

      ```shell
      $ ls -a
      ```

   4. 删除 .git

      ```shell
      $ rm -rf .git
      ```

   5. 可以看到master分支已经删除

      ```shell
      $ ls -a
      ```





### NPM

> node package manager ：NODE模块管理工具，根据NPM我们可快速安装、卸载所需要的资源文件（例如：jQuery、vue、vue-router...）
>
> 
>
> 去NDOE官网：https://nodejs.org/zh-cn/ 下载NODE（长期支持版），安装NODE后，NPM也跟着安装了

```shell
$ node -v
$ npm -v  出现版本号证明安装成功
```

#### 基于NPM进行模块管理

> https://www.npsjs.com