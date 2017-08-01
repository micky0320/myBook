#### 列出标签
`git tag`
查看所有tag

#### 添加标签
`git tag -a [version] -m [information]`
创建附注标签时，`-a`即annotated的缩写，指定标签类型，后附标签名。`-m`指定标签说明，说明信息会保存在标签对象中。
例如：`git tag -a test0.1.1 -m '0.1.0测试环境xxxx'`

#### 查看标签及注释信息
`git tag -l -n`
查看所有tag和tag的对应注释信息

#### 切换到标签
同切换分支一样，`git checkout [tagName]`

#### 查看标签及修改
`git show [tagName]`

#### 删除标签
`git tag -d [tagName]`
`-d`是delete缩写

#### 删除远端库的标签
`git push MAgit :refs/tags/[tagName]`   注意：“:” 前面要有空格
例：`git push MAgit :refs/tags/test0.2.1`

#### 发布标签
通常的git push不会将标签对象提交到git服务器，我们需要进行显式的操作：
- `git push origin v0.1.2` # 将v0.1.2标签提交到git服务器
- `git push origin –-tags`  # 将本地所有标签一次性提交到git服务器

#### 删除本地branch
`git branch -d/D [branchName]` (大写的D可以强制删除branch) 
例子：`git branch -d alpha`或`git branch -D alpha`

#### 删除远端branch
`git push origin :[branchName]` 注意：“:” 前面要有空格 
例子：`git push origin :alpha`

#### 重命名分支
`git branch -m deve develop` deve是旧分支名称，develop是新分支名称
##### 需要再把远端旧分支删去，否则只是将本地分支改名，在远端新建了一个分支
