
## Git Commit message 的格式规范（[参考](https://segmentfault.com/a/1190000009048911)）

每次提交，Commit message 都包括三个部分：header，body 和 footer。
```git
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```
[中文参考](https://juejin.im/post/5b4328bbf265da0fa21a6820)
```

# 标题行：50个字符以内，描述主要变更内容
#
# 主体内容：更详细的说明文本，建议72个字符以内。 需要描述的信息包括:
#
# * 为什么这个变更是必须的? 它可能是用来修复一个bug，增加一个feature，提升性能、可靠性、稳定性等等
# * 他如何解决这个问题? 具体描述解决问题的步骤
# * 是否存在副作用、风险? 
#
# 如果需要的化可以添加一个链接到issue地址或者其它文档
```
### Header
包括三个字段：`type`（必需）、`scope`（可选）和`subject`（必需）。
#### type
说明 `commit `的类别，只允许使用下面7个标识
* `feat`: 新特性，新功能
* `fix`: 修复`bug`
* `docs`: 仅修改了文档
* `style`: 仅仅修改了空格、样式、格式缩进、逗号等等，不改变代码逻辑，不是 `css` 修改
* `refactor`: 代码重构，没有加新功能或者修复bug
* `test`: 测试用例修改
* `chore`: 改变构建流程、或者增加依赖库、工具等
#### scope
用于说明 `commit` 影响的范围，比如数据层、控制层、视图层等等,如果修改影响了不止一个scope，可以使用*代替。
#### subject
` commit` 目的的简短描述，不超过50个字符。

其他注意事项：

* 以动词开头，使用第一人称现在时，比如change，而不是changed或changes

* 第一个字母小写

* 结尾不加句号（.）
### Body
是对本次 `commit` 的详细描述，可以分成多行。

注意点:

* 使用第一人称现在时，比如使用change而不是`changed`或`changes`。

* 第2行是空行

* 应该说明代码变动的动机，以及与以前行为的对比
### Footer
用于以下两种情况：

#### 不兼容变动
如果当前代码与上一个版本不兼容，则`Footer`部分以`BREAKING CHANGE`开头，后面是对变动的描述、以及变动理由和迁移方法。

#### 关闭Issue
如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue 。
**分支名规范**： 
feature/xxx xxx代表需要做的事情

### [Git简易操作](http://www.bootcss.com/p/git-guide/)
#### 1.新建`git`仓库
创建新文件夹，打开，然后执行 `git init`，创建新的`git`仓库
#### 2.检出仓库
创建一个本地仓库的克隆版本：`git clone /path/to/repository`
#### 3.工作流
本地仓库由`git`维护的三棵树组成：
* 工作目录：持有实际文件
* 暂缓区(`Index`)：缓存区域，临时保存改动
* `HEAD`：指向最近一次提交后的结果
#### 4.添加与提交
* 添加到缓存区：
  * `git add <filename>`提交指定文件
  * `git add*`：提交所有文件
* 实际提交：`git commit -m "代码提交信息"`
这时提交到`HEAD`，但未到远程仓库
#### 5.推送改动
提交到远程仓库：`git push origin <分支名>`
如果报错，可以试试先pull更新合并一下本地仓库代码：`git pull`
#### 6.分支
在创建仓库的时候，`master` 是“默认的”。在其他分支上进行开发，完成后再将它们合并到主分支上。
* 创建分支并切换过去：`git checkout -b <分支名>`
* 切换回主分支：`git checkout master`
* 删掉新分支：`git branch -d <分支名>`
* 分支未推送到远程仓库，不为他人可见

#### 7.更新与合并
* 更新本地仓库：`git pull`
* 在工作目录中获取(`fetch`)并合并(merge)远程的改动，合并其他分支到当前分支：`git merge <branch>`

两种情况下，`git `都会尝试去自动合并改动。

不幸的是，自动合并并非次次都能成功，并可能导致 冲突（`conflicts`）。 

这时候就需要自己修改这些文件来人肉合并这些 冲突（`conflicts`） 了。

改完之后：
`git add <filename>`

合并改动之前，可以查看：
`git diff<source_branch> <traget_branch>`
