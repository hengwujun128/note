## 1.如何在 sourceTree 中进行版本回退撤销 commit

- bash command

```
//  已经提交(代码进入本地仓库)，但是没有推送
// origin/master 代表远程仓库，从远程仓库把代码拉回来
git reset --hard origin/master


// 已暂存，未提交
git reset           //回到已修改，未暂存状态
git reset --hard    //回到原始状态，未修改状态

// 已推送
git reset --hard HEAD^
```

- sourceTree 处理（已提交，未推送）

```
第一步：选中提交之前的版本
第二步：然后右击，reset master to this commit
第三步：会退到暂存区，会退到未暂存，会退到未修改三种情况
```

[参考](https://blog.csdn.net/gang544043963/article/details/71511958)
