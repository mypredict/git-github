工作区 : 代码

暂存区 : 打算提交的东西还没有提交

本地库 : 存储每个提交的历史版本

基本命令 :
  1.git status 查看状态
  2.vim <文件> 编辑文件内容
  3.:wq 退出编辑
  4.cat <文件> 查看文件内容

本地库初始化:
  1.初始化
    git init 产生 .git 文件目录, 存放本地库相关的文件
  2.设置本地库签名:
    项目权限(存放在 .git/config 文件下): 
      git config user.name xx
      git config user.email 110@qq.com
    系统权限(存放在 c/user/yourname/.gitconfig):
      git config --global user.name xx
      git config --global user.email 110.@qq.com
    项目权限优先级大于系统


操作本地库:
  1.添加到暂存区
    git add <文件 | .(代表所有)>
  2.从暂存区移除
    git rm --cached <文件>
  3.提交并输入提交信息(记录日志注释)
    git commit -m "这是我的第一次提交" <要提交的文件, 不写默认所有缓存区文件都提交>
    git commit -am "这是直接添加所有文件然后提交时做的描述" 相当于上面的1(.)和3步骤


查看提交记录:
  1.git log
    哈希值标识, 分支指向, 时间等
    日志过多可用空格向下, b向上, q退出换页
  2.git log --pretty=oneline
    简洁显示
  3.git log --oneline
    更简洁
  4.git reflog
    标识出了移动的步骤数


版本的前进后退:
  1.git reset --hard <hash索引>
  2.git reset --hard HEAD^ 后退1步(有几个^退几步)
    git reset --hard HEAD~n 后退n步
  3.git reset --soft HEAD 本地库移动HEAD
  4.git reset --mixed HEAD 本地库和缓存区移动HEAD


删除文件及找回:
  1.rm <文件> 删除文件
    git add <文件> 提交到缓存区
      git reset --hard HEAD 再还没有提交到本地库的时候可以通过这个重置缓存区
      git commit -m "删除文件的记录" <文件>
  2.git reflog 查看记录是可以看到记录的
    git reset --hard <hash索引> 还是能找到


文件比较:
  1.git diff <文件> 将工作区中文件和暂存区中的进行比较
  2.git diff <hash索引> <文件> 将工作区中文件和历史记录进行比较


分支:
  git branch -v 查看分支情况
  git log --graph 图表形式查看分支情况
  git branch <分支名> 创建一个分支
  git checkout <分支名> 切换分支
  git merge <要被合并的分支名> 合并分支, 合并到上面checkout选中的分支上
  <<<<<<<
  =======
  分支冲突手动解决
  git add <文件名>
  git commit -m "提交日志" 这时不能再加文件名, 直接提交解决冲突


远程库操作:
  地址别名: git remote add <别名> <真实地址>
  git remote -v 查看地址情况
  git push -u origin master 将本地库中的master分支推送到github远程库
  git clone <远程库地址> 将远程库内容复制过来
  git fetch origin master 将远程库中的master分支抓取下来, 但是不做本地合并
  git checkout master 指针切换到本地要合并的master分支
  git merge origin/master 将远程master分支合并到上面的本地master分支
  git pull origin master 抓取及合并 fetch + merge

邀请协同开发:
  Settings > Collaborators > [被邀请人email或者名称] > 转到链接加入
  操作冲突时先拉取下来更改再上传, 同上本地
  跨团队: fork > 修改提交到远程库 > Pull requests > New pull request > create pull request
  主团队: Pull requests > merge pull requests 合并完成