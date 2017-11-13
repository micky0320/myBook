## revert & reset & checkout 比较

### git checkout

```
参数
-- 文件名：撤消此文件提交
[branch]: 切到此branch
```

撤消文件操作
```
git add src/index.js
git checkout -- src/index.js
```

### git reset 
```
参数 
HEAD: 表示当前分支，
HEAD^: 上一个版本 
HEAD^100: 前100个版本
```
代码提交到存储库,使用reset可撤消此文件在存储库的修改，文件回到缓存区

```
git add src/index.js
git ci -m 'modify index.js'
git reset HEAD^
```

### git revert
使用于远端库回退版本，回退后<code>git push</code>,提交此次存储库数据

```
eg:
git revert [commitId]  // commitID 提交id；
撤消对应ID的此次提交记录，并新生成一次提交，
```

### git cherry-pick

<code>git cherry-pick <commit id></code>用于把另一个本地分支的commit修改应用到当前分支，
  可以跨分支，如从A分支取出commit的修改作用于B分支，再进行代码合并。


