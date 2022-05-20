# Git常用命令

## 基本操作

- 初始化仓库
  - `git init [dirname]`

- 查看仓库的状态
  - `git status`
- 向暂存区中添加文件
  - `git add [filename]`
  - 如果想要将所有文件添加在暂存区就是用*

- 将暂存区中的修改提交到本地仓库
  - `git commit -m "commit message"`
  - 是用-m参数可以提交一行简洁的描述信息,但是如果想要记录更加详细的信息,就不要加-m
    - 详细记录信息一般格式如下
      - 第一行：用一行文字简述提交的更改内容
      - 第二行：空行
      - 第三行以后：记述更改的原因和详细内容

- 查看提交日志
  - `git log`
  - 只显示第一行的简短信息日志
    - `git log --pretty=short`
  - 显示指定目录与文件的日志
    - `git log filename`
  - 查看提交带来的改动
    - `git log -p`
  - 图表查看更加细致的日志
    - `git log --graph`
- 查看更改前后的差别
  - 查看工作树与暂存区的差别
    - `git diff`
  - 查看暂存区与本地仓库的差别
    - `git diff HEAD`
- 从现有仓库克隆
  - `git clone <repository>`

## 本地仓库配置

- 查看当前仓库配置信息
  - `git config --list`
  
- 配置本地用户信息
  
  - 设置用户名
    - `git config --global user.name "username"`
  
  - 设置邮箱
    - `git config --global user.email emailaddress`
    - `--global`参数表示设置全局配置
    - 还可以设置系统`--system`配置
    - 也可以设置本地`--local`配置
    
    

## 分支管理

- 显示所有分支
  - `git branch`
  - 指定路径克隆到指定目录
  - `git clone <repository> <directory>`
- 切换分支
  - 一下三种方式效果一致
  - `git checkout -b branchname`
  - `git branch branchname`
  - `git checkout branchname`
- 切换至上一个分支
  - `git checkout -`
- 合并分支
  - `git merge --no--ff branchname`
    - `--no--ff`参数表示创建合并提交信息

## 版本管理

- 版本回退,回退到某一次提交的版本
  - `git reset [--soft | --mixed | --hard] [HEAD]`



## 远程仓库操作

- 配置远程仓库

  - `git remote add [shortname] [url] `

  - ```
    git remote add origin git@github.com:tianqixin/runoob-git-test.git
    ```

- 删除远程仓库
  - `git remote rm name`
- 重命名远程仓库
  - `git remote rename old_name new_name`
- 从远程仓库获取代码库
  - `git fetch`
- 下载远程代码并合并
  - `git pull`
- 上传远程代码并合并
  - `git push`