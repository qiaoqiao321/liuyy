---
draft: false
---

# git 常用命令总结

先附上一张git 的工作原理图：

![image-20221020193203670](C:\Users\qiaoqiao\AppData\Roaming\Typora\typora-user-images\image-20221020193203670.png)

## 1、初始化仓库

```text
git init
```

## 2、添加本地所有代码，添加到暂存区

```text
git add .
```

## 3、提交代码描述

```text
git commit -m '增加新的功能'
```

## 4、添加远程仓库，将远程仓库命名为 origin

```text
git remote add origin git@github.com:xxxx/xxx.git
```

## 5、初始化推送

-u 的含义是将本地仓库关联到远程仓库，简单来说，带上`-u` 参数其实就相当于记录了push到远端分支的默认值，这样当下次我们还想要继续push的这个远端分支的时候推送命令就可以简写成`git push`即可

```text
git push -u origin master
```

## 6、提交到主分支

```text
git push origin master
```

## 7、创建分支

```text
git checkout -b  <branchname>  # -build
```

## 8、查看分支

```text
git branch   
```

## 9、提交到分支

`git push origin dev`:将本地的dev 分支push到远程的dev 分支（不是将当前分支！！！！！！！！！！！！！）

如果本地分支与远程分支不同名，那么用这个就会报错。正确命令如下：
1.首先将本地与远程分支成功追踪（track）：
git branch --set-upstream-to=origin/dev_remote:当前分支与远程dev_remote分支绑定
2.推送到远程，注意方式不一样，要多一个 " head: "，后面跟分支名
git push origin head:dev_remote
如果在使用了--set-upstream-to 后要推送到同名分支，可以直接使用git push origin head命令

```text
git push origin <barnchname>
```

## 10、删除分支

```text
git checkout -d  <branchname>   #-delete
git branch -d <branchname>      #-delete
```

## 11、切换回主分支

```text
git checkout master
```

## 12、合并分支，将< branchname >的分支合并到当前分支上

```text
git merge <branchname>
```

## 13、冲突的产生，检测冲突的原理

每一行代码，都会对应一个commit信息,每个commit都会指向一个或者多个父节点的commit。

merge代码的时候，如果新进来的这行代码，和你原有的这行代码，两个commit信息不同了，那么git就会开始找这俩的关系，

如果commit A 和 B 是父子关系，那么就不会冲突，否则会冲突，比如兄弟关系。

## 14、pull request 和 merge request 的区别

pull request : 小明写完代码了想合入到原作者的仓库，新建了一个“pull request”，拉请求？这明明是推啊，小明将自己的修改推到原作者的仓，感觉叫“push request”比较合适吧

merge request : 团队中每个人都从远程仓库 develop 分支拉取代码，本地基于 develop 分支新建特性分支，修改完代码将特性分支推到远程仓，紧接着新建 Merge Request 期望将自己的特性分支合入 develop 分支。从上面这个流程来看Merge Request 就是将自己的特性分支合入到主干分支。
