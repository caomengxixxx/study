#### git

##### 1、分布式版本控制工具

##### 2、git结构

###### 工作区		写代码

###### 暂存区		临时存储

###### 本地库		历史版本

![image-20210105200813845](C:\Users\caomengxi\AppData\Roaming\Typora\typora-user-images\image-20210105200813845.png)

##### 3、代码托管中心

- 局域网
  - GitLab服务器

- 外网
  - GitHub
  - Gitee

##### 4、团队外的人参与开发

![image-20210105201008760](C:\Users\caomengxi\AppData\Roaming\Typora\typora-user-images\image-20210105201008760.png)

##### 5、初始化

###### 初始化仓库

```bash
# 在项目所在目录下执行git init可以初始化一个仓库
git init
# 注意事项：.git目录中存放的是本地库相关的子目录和文件，不要删除，也不要胡乱修改
```

###### .git的目录

![image-20210105202348451](C:\Users\caomengxi\AppData\Roaming\Typora\typora-user-images\image-20210105202348451.png)



##### 6、设置签名

###### 形式

- 用户名：caomengxi

- 邮箱地址：1366090512@qq.com

###### 作用

- 区分不同的开发人员的身份

###### 优先级

- 项目级别/仓库级别：仅在当前本地仓库范围有效(配置信息放在config中)
  - git config user.name caomengxi_pro
  - git config user.email 1366090512@qq.com
- 系统用户级别：登录当前操作系统的用户范围(配置信息放在.gitconfig中)
  - git config --global user.name caomengxi_glb
  - git config --global user.email 1366090512@qq.com
- 就近原则，有项目级别的话，按照项目级别的来

##### 7、基本操作

```bash
# 查看状态，查看工作区，暂存区的状态
git status

# 添加，将新建和修改添加到暂存区
git add 文件名

# 提交，将暂存区的内容添加到本地库
git commit -m "备注信息" 文件名

# 查看提交日志
git log
# 提交日志以一行的形式显示
git log --pretty=oneline 
git log --oneline # hash值只显示一部分
git reflog # 记录版本切换的步数
```

##### 8、版本切换

###### 基于索引值操作

```bash
git reset --hard 局部索引值
```

###### 使用^符号（只能后退）

```bash
git reset --hard HEAD^^^ # 后面有几个^就是后退几个版本
```

###### 使用~符号（只能后退）

```bash
git reset --hard HEAD~3 # 数字为多少，就是后退几个版本
```

##### 9、参数对比

```bash
--soft
# 仅仅在本地库移动HEAD指针
--mixed
# 在本地库移动HEAD指针
# 重置暂存区
--hard
# 在本地库移动HEAD指针
# 重置暂存区
# 重置工作区
```

##### 10、删除文件并找回

```bash
# 删除文件
rm 文件名

# 前提：删除前，文件存在时的状态提交到了本地库
# 操作：
git reset --hard [指针位置]
# 删除操作已经提交到本地库：指针位置指向历史记录
# 删除操作尚未提交到本地库：指针位置使用HEAD
```

##### 11、比较文件差异

```bash
git diff [文件名]
# 将工作区中的文件和暂存区进行比较

git diff [本地库中历史版本] [文件名]
# 将工作区中的文件和本地库历史记录比较

git diff
# 不带文件名比较多个文件
```

##### 12、分支操作

###### 创建分支

```bash
git branch [分支名]
```

###### 查看分支

```bash
git branch -v
```

###### 切换分支

```bash
git checkout [分支名]
```

###### 合并分支

```bash
# 第一步：切换到接受修改的分支（被合并，增加新内容）上
git checkout [接收合并分支名]
# git checkout master
# 第二步：执行merge命令
git merge [有新内容的分支名]
# git merge hot_fix
# 这样子就把hot_fix合并到master中了
```

###### 解决冲突

```bash
# 第一步：编辑文件，删除特殊符号
# 第二步：把文件修改到满意的程度，保存退出
# 第三步：git add [文件名]
# 第四步：git commit -m "日志信息" # 一定不能带具体文件名
```

##### 13、给远程仓库起别名

```bash
# 查看远程仓库
git remote -v

# 起别名
git remote add origin https://github.com/tyrion777/test.git

# 查看
git remote -v
# origin  https://github.com/tyrion777/test.git (fetch)
# origin  https://github.com/tyrion777/test.git (push)

```

##### 14、推送

```bash
# 推送
git push origin master
```

##### 15、克隆

```bash
# 克隆
git clone 远程地址

# 完整的把远程库下载到本地
# 创建origin远程地址别名
# 初始化本地库
```

##### 16、邀请成员加入

```bash
远程库中的settings 邀请一个合作者 即可共同开发
```

![image-20210106210201463](C:\Users\caomengxi\AppData\Roaming\Typora\typora-user-images\image-20210106210201463.png)

##### 17、pull

```bash
# pull = fetch + merge

git fetch [远程库地址别名] [远程分支名]
git merge [远程库地址别名/远程分支名]
git pull [远程库地址别名] [远程分支名]

# 没有本地库的时候，一定先从远程库中克隆，克隆下来之后就是本地库的状态了，想要提交代码的话，需要进入团队，才能提交代码
```

##### 18、解决冲突

```bash
# 提交的时候，一定要先拉取最新的，如果有冲突，手动合并，达到要求的效果，没有冲突的话，pull相当于是fetch和merge的功能，没有冲突的话，就直接提交就行

# 较为官方的总结
# 如果不是基于GitHub远程库的最新版本所做的修改，不能推送，必须先拉取
# 如果拉取下来后进入冲突状态，则按照 分支冲突解决 即可。
```

##### 19、多人协作开发

```bash
# 我的理解
# 小明从远程库中拉取了一次代码，然后去解决冲突，这时候，小王也从远程库拉取了一次代码，然后没有冲突，直接就提交了。然后小明提交失败，这时候只能现在拉取一次最新的代码，解决完冲突之后，才能再次提交。（永远都是最新的版本才能提交）
```

##### 20、跨团队开发

```bash
fork
# todo
```

##### 21、ssh免密码登录

```bash
# 切换到家目录
cd ~

# 生成
ssh-keygen -t rsa -C 1366090512@qq.com

# 进入.ssh
cd .ssh

# cat id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC67iPf1bDYo5SdM90fMokTv7TtBWJhxCwYE+PGSqvZC0bjb6mbYnUv4mpa4+1TlLzYRnSKHnz8uysoh7Vz45EoaBCN3MVA5cpXy3YfIuYDqK1wuYBWOJgtYrJGfViNMd08qX5zDQqThNkp7ljD8T7YcJBs/FMlriiBQaGitHZPMev6K0uzg80lMOY0KB1ehEliH1GfpU1EleZ3BofFQ6x4tZnuK1g3o/i/7vkVOiy4FciDYj2jSdFXqxHfSAX65Lc8yRB0mz0HcMpxGF2BaOJ1eMn0dLq0nvlVUMJDPxGlioFHj0//sxsEZ5FTzWEfgN6t7eEHMun19K/6UmZtYAn9uJQy9FKsKej1MhgS1RPumfsis1yUzec0W/U9ijdssBscUjwwEn7rNEjsSsBZwJ2ru4pGykZgHnXxyg742+MutICNAgPJgLwIWYrIrMxaXtx46zLqW3qOxehEujZ31GwplNn+fyyf9ZiEtaQKSYffvIkAric8aizocvFIBka2Yw8= 1366090512@qq.com

# 起别名
git remote add origin_ssh git@github.com:tyrion777/studynote.git

# 测试push
git push origin_ssh master
```

##### 22、idea中的操作

```bash
# todo
```

##### 23、GitLab搭建

```bash
# 官网
https://about.gitlab.com/install/#centos-7

# 部署好之后，直接访问ip地址即可
106.14.20.157
```

##### 24、集成idea

```java
// 为什么要忽略.idea,.iml等文件，因为无法保证团队里面的人使用同一款ide开发工具，所以一些配置文件会发生冲突，（重要的很）

// 在vcs中创建git的本地库，选中总的项目，即可创建一个本地库（基操）

// 
```

