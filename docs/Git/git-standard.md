# git 规范

git commit的信息使用了commitlint（@see https://github.com/conventional-changelog/commitlint#getting-started, https://github.com/conventional-changelog/commitlint#config）

## 常用的的Commit message 的格式
```bash
type(scope?): subject  #scope 是可选的
```
## 完整的Commit message 的格式
```bash
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```
其中，Header 是必需的，Body 和 Footer 可以省略。
Header Header 部分只有一行，包括三个字段：type（必需）、scope（可选）和 subject（必需）。

+ type

    type 用于说明 commit 的类别，只允许使用下面标识

    + release:合并上线

    + feat:新功能特性

    + fix:bug 修复

    + docs:文档变更

    + style:样式--不影响代码含义的更改(空白、格式、缺少分号等)

    + refactor:重构--既不修复 bug 也不添加特性的代码更改

    + perf:重构--改进性能的代码更改

    + test:添加缺失的测试

    + chore:对构建过程或辅助工具和库的更改

    + revert:还原到提交

+ scope

    scope 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

+ subject

    subject 是 commit 目的的简短描述，不超过 50 个字符。


## 成功提交的例子
> 一般来说，模式大多如下

```bash
$ git commit -m"fix(server): send cors headers"
$ git commit -m"fix(家庭页面): 修复家庭页面xxx的bug"
$ git commit -m"chore: 优化脚手架"
```

> 如果要定义header，body，footer，建议用git-cz，代码配置的命令如下

```bash
$ yarn commit
// 或者
$ npm run commit
// 或者（需要安装commitizen）
$ git-cz
```