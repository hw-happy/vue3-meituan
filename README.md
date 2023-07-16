# vue3-meituan
这是一个仿美团的项目
 
采用了vue3框架和vant4组件库

当前分支main分支

1、
测试git名称 修改当前仓库的user.name 点进远端clone下来的文件中右键 git bash 
通过 git config user.name 查看当前用户名 
    git config user.name "HW" 设置用户名 在这个项目的每一次远程操作 都会显示

2、github项目push出现443 因为在C:\Windows\System32\drivers\etc下的hosts文件添加了有关github的加速项 
        140.82.112.4 github.com
        199.232.69.194 github.global.ssl.fastly.net
删除掉就可以进行本地推送远端了，但是访问github可能会出现缓慢。所以在推送完之后再写回去。

##  企业推送实际操作
在其他分支开发，代码要合到dev上时
1.先切到dev分支，执行git pull --rebase，拉取dev最新代码
2.切回到开发分支，执行git rebase dev，把dev分支代码合到开发分支。如有冲突则解决冲突，解决完执行git rebase --continue。rebase完的代码采用git push --force推到开发分支上。（注意这个--force会强行覆盖远端分支，强推前确保远端分支上跟本地分支比没有新的提交了，不然会把远端新提交覆盖。如果远端有新提交，采用git fetch方法先把新提交拉到本地，再用cherry-pick方法捡取到本地分支，再强推）。
# 不推荐直接force 使用 git push --force-with-lease
3.切回dev分支，复制开发分支上要合并到dev的提交的提交号，执行git cherry-pick 提交号，把开发分支上的提交捡取到dev分支上。如果多个连续的提交，可以采用git cherry-pick  起始提交号^..终止提交号 来批量捡取。
4.代码捡取到dev分支后，dev分支上执行git push把代码推上dev即可。
 后续代码提交也采用 先rebase再cherry-pick的方式吧，不用merge的方式了，这样提交会保持在一条线上，我们平台其他项目都是这样的方式的，你们刚好也熟悉熟悉这种方式。