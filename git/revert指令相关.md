## revert & reset & checkout 比较

### git checkout [options]

```
options:
-- 文件名：撤消此文件提交
[branch]: 切到此branch
```

撤消文件操作
```
git add src/index.js
git checkout -- src/index.js
```

### git reset [options]
```
options: 
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

### git revert [options]
使用于远端库回退版本，回退后<code>git push</code>,提交此次存储库数据

```
eg:
git revert [commitId]  // commitID 提交id；
撤消对应ID的此次提交记录，并新生成一次提交，
```
