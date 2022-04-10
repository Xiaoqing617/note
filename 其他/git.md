1. 安装git

   官网下载，一路默认选择安装

2. 绑定自己的邮箱和名字

   git config --global user.name "账号名字"

   git config --global user.email "邮箱"

3. 初始化一个仓库，会在当前目录下新建.git隐藏文件夹

   git init

4. 查看文件的状态，红色表示在工作区，绿色表示已将放在暂存区，什么都没有表示已将上传到仓库

   git status

   git status -s   (简化的日志信息)

5. 把文件提交到暂存区

   git add ./（./是需要提交的文件路径  ./代表根目录全部）

6. 把暂存区所有文件提交到仓库，必须要有提交的说明信息，如果是第一次提交没有绑定邮箱需要绑定

   git commit -m '提交的说明信息'

   git commit -a -m '提交的说明信息'    （如果是一个已经暂存过的文件可以使用这个命令快速提交，不用再git add）

   git commit --anend -m '提交的说明信息'（修改最近一次的提交说明信息，如果提交的说明信息写错了使用此命令）

7. 查看提交的记录

   git log

   git log --oneline  (简化的日志信息)(以上两个只能查看当前版本以及在它之前的版本的信息)

   git reflog  (查看所有的提交信息)

8. 版本回退，将代码回复到已经提交的某一个版本中（一般不用，回退之前记得将本地的代码另存一份）

   git reset --hard 版本号  （使用git log可以查看版本号）

   git reset --hard head~1  (回退到前一个版本)

9. 忽视文件，如果有不需要上传的文件需要创建一个.gitignore文件用于写不要上传的文件名

   比如再.gitignore中写node_modules，表示不需要上传node_modules

10. 分支（第一次提交代码会自己创建一个master分支）分支实质上是一个指针

   1. git branch  (查看当前所有本地分支)
   2. git branch -a   （查看当前全部（本地、远程）分支）
   3. git branch 分支名    （创建一个分支）
   4. git checkout 分支名  （切换到某个分支）
   5. git checkout -b 分支名   （创建并切换分支）
   6. git merge 分支名  （将其他分支合并到当前分支）
   7. git branch -d 分支名   （删除分支，注意必须在其他分支中才能删除这个分支）

11. 远程仓库

    1. git clone 远程仓库地址    （克隆远程仓库的代码到本地）
    2. git push 仓库地址 maste    （将本地仓库的代码提交到远程仓库，git push -u 仓库地址 maste 可以将这个地址变为默认，以后只需要输入git push maste即可上传到这个地址）
    3. git pull    （从远程仓库上拉取更新）
    4. git remote 自定义名字 地址    （可以将地址存在这个名字中，下次使用地址只需要输入名字即可，默认带有origin      ，使用git remote可以查看所有的名字）
    5. ssh免密码配置
       1. 桌面右击选择Git Bash Here在里面输入ssh-keygen -t rsa回车
       2. 一路下来不用输入直接回车，第一次可能会输入一个y确认
       3. 在显示的目录中找到自己生成的钥匙
       4. id_rsa是私钥，id_rea.pub是公钥，需要给GitHub公钥
       5. 在GitHub账号设置中点击SSH然后new一个钥匙输入公钥中的东西即可

