# git基本操作

## git配置

* 初次运行git时对git的配置 

    `git config --global user.name "<your github name>"`
    `git config --global user.email <your github email>`

* clone远程仓库的项目到本地 

    `git clone https://github.com/username/example.github.io.git`

## 基本命令

    git status // 查看当前项目下的状态
    git remote -v//查看当前项目远程连接的是哪个仓库地址
    git push -u origin master // 将本地的项目提交到远程仓库中

## 上传本地文件到远程仓库

    git add .
    git commit -c "commit information"
    git push

## 同步远程仓库到本地

    git fetch origin master
    git log -p master..origin/master 
    git merge origin/master

上述命令首先从远程的origin的master主分支下载最新的版本到origin/master分支上然后比较本地的master分支和origin/master分支的差别最后进行合并。

**如果想强制合并本地项目可使用以下命令**

    gitfetch--allgitreset--hardorigin/mastergitfetch

---

## 如果项目中删除了一些文件,如何提交

    git status 
    git add . 
    git rm your/file/path
    git rm folder/path -r // 删除该目录下的所有文件(包括目录)

## 使用代理

#### 使用sock5

	git config --global http.proxy "sock5://127.0.0.1:1080"
	git config --global https.proxy "sock5://127.0.0.1:1080"

#### 使用http

	git config --global http.proxy "http://127.0.0.1:1080"
	git config --global https.proxy “https://127.0.0.1:1080"

#### 取消代理

	git config --global --unset http.proxy 
	git config --global --unset https.proxy 
	
## 保存用户名密码（以便push时不用多次输入）

#### 使用http/https协议

* 设置记住密码（默认15分钟）：

	git config --global credential.helper cache
	
* 如果想自己设置时间，可以这样做：

	git config credential.helper 'cache --timeout=3600'

这样就设置一个小时之后失效

* 长期存储密码：

	git config --global credential.helper store

* 增加远程地址的时候带上密码也是可以的。(推荐)

	http://yourname:password@git.oschina.net/name/project.git
	
补充：使用客户端也可以存储密码的。

#### 使用ssh协议

如果你正在使用ssh而且想体验https带来的高速，那么你可以这样做： 

* 切换到项目目录下 ：

	cd projectfile/
	
* 移除远程ssh方式的仓库地址

	git remote rm origin
	
* 增加https远程仓库地址

	git remote add origin http://yourname:password@git.oschina.net/name/project.git
	
## 关联本地工程到github仓库

    git init  //地仓库初始化，执行完后会在工程目录下生成一个.git的隐藏目录
    git add .   //添加所有文件到本地索引，命令用法：git add <file>
    git commit -m "My first commit operation"   //提交修改到本地仓库，-m选项添加提交注释
    git remote add origin git@github.com:yihao31/yihao31.github.io.git  //添加远程仓库地址，保存在origin变量中
    git push origin master   //按照前一条命令中origin给定的github地址推送到github仓库的master分支

# 使用github 管理分支

## 本地的分支管理

    git branch dev  // 创建一个名为dev的分支
    git checkout dev  //切换分支
    git branch //查看当前已有的分支信息,并且在当前所在分支高亮 

**为什么要创建分支?**

比如某天想搞些新事情了,可以创建一个名为debug的分支在上面调试修改,这样如果失败了也不会影响到origin branch,而调试成功了也可以直接合并: 

	+ 建立一个新分支:  
	```
    git checkout  -b debug 
	```

    + 如果最后没有调试成功,可以选择留着debug分支,也许以后有灵感了再来弄(代码注释一定要做好),但是如果就不想弄了也可以选择删除分支: 
    ```
    git brach -d debug
    ```
    + 如果算法调试成功了,想合并到master中:
    ```
    git checkout master // 切换到master branch
    git merge debug // 合并debug 到master
    ``` 
    

**注意:** 合并发生冲突是常有的事情,因此一旦出现类似下面的提示,就得自己手动解决按冲突了

    CONFLICT (content): Merge conflict in...
    Automatic merge failed; fix conflicts and then commit the result.

git会使用下面的格式提醒用户哪里有冲突:

    <<<<<<<HEAD
     master原有的内容
    ======= debug分支中冲突的内容
    >>>>>>>debug

如果比较感兴趣想看看git是怎么记录合并的,可以使用底下的命令:

    gitlog--graph--pretty=oneline--abbrev-commit

# Appendix

**Local**：

    git clone git@github.com:xiahouzuoxin/mp3-encode.git        # 在本地克隆一个github上仓库
    git status                    # 获得当前项目的一个状况
    git commit -a              # 将修改文件（不包括新创建的文件）添加到索引，并提交到仓库
    git add [file]                # 添加文件到本地索引
    git branch                  # 获得当前仓库中所有分支列表
    git branch zx-branch                # 新建本地一个名为zx-branch的分支，主分支名为master
    git branch -D branch_name     # 删除名称为branch-name的本地分支
    git checkout master                  # 切回主分支，切换到zx-branch只需要将master改成zx-branch
    git log# 查看提交日志，有许多附加参数
        git log -p                               # 显示补丁
        git log--stat                          # 日志统计：那些文件修改了，修改了多少行内容
        git log--graph                       # 使日志看上去更漂亮
    git diff master..zx-branch           # 比较两个分支之间差异
    git remote rm origin                   #  删除origin变量地址
    
    git branch [name]                 # 创建本地分支，注意新分支创建后不会自动切换为当前分支
    git checkout [name]              # 切换到name分支
    git checkout -b [name]          # 创建name分支并切换到name分支
    
    git merge [name]                  # 将name分支与当前分支合并，name可以是远程分支，如origin/master

**Remote**:

    git push origin [name]          # 创建远程name分支
    git push origin:zx-branch      # 删除远程origin仓库地址的zx-branch分支 
    git branch -r                         # 获得当前仓库中所有分支列表，即查看远程分支

