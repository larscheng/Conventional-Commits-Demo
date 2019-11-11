# 前言

本文为介绍约定式提交，主要从以下几点展开：

- [现状分析]()
- [约定式提交]()
    - [优点]()
    - [规范]()
- [commitizen]()
- [standard-version]()

本文对应的github项目地址：https://github.com/larscheng/Conventional-Commits-Demo

# 现状分析

目前我们的项目在commit时基本上五花八门，各领风骚。虽然不如网上的那些恶搞commit记录，但是这一现象严重影响我们在阅读记录和查找bug原因时的效率。


我们可以感受下：


![真实项目commit记录](https://cdn.jsdelivr.net/gh/larscheng/myImg/blogImg/commit/20191111163609.png)


可以对比看看同样按照规范式提交的项目的commit记录

![](https://cdn.jsdelivr.net/gh/larscheng/myImg/blogImg/commit/20191111165841.png)


> 两种commit message的对比很明显说明了情况，统一的提交信息，不仅看起来舒服，而且读起来更舒服


其实已经越来越多的人开始意识到规范化提交的重要性，据我在公司实地采访了一圈，前端团队早已经开始`约定式提交`，这也可能是因为目前社区中主流的提交规范都是由[Angular提交准则](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md)形成。


> **为了提高开发效率，减少在处理问题时耗费的时间，推荐大家在写完代码，提交时能够使用以下规范：**

- 规范化提交(不一定是文中提到的方式,但无论哪种方式，要做到`统一`、`简明`)
- 一处变更一次commit(谨防多处、多次修改堆积成一次commit提交，这对后期bug分析将是灾难)





# 约定式提交

约定式提交：每次使用`git commit` 的时候都需要写commit message,如果message的 style是`按照固定的模版格式书写`，对于后期的维护和编写changelog都有巨大的好处。 

而且现在的很多自动生成changelog的工具，都是建立在约定式提交的基础之上。

## 优点

- 可读性好，清晰，不必深入看代码即可了解当前commit的作用。
- 为 Code Reviewing做准备
- 方便跟踪工程历史
- 让其他的开发者在运行 git blame 的时候想跪谢
- 提高项目的整体质量，提高个人工程素质

## 约定式提交规范

[约定式提交规范](https://conventionalcommits.org/lang/zh-Hans)是基于[Angular提交准则](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md)形成，提交说明的结构如下：

```
<类型>([可选的作用域]): <描述>
// 空一行
[可选的正文]
// 空一行
[可选的脚注]
```

其中，`<类型>`是为了向类库使用者表明其意图，其可选值为：

- feat: 表示新增了一个功能
- fix: 表示修复了一个 bug
- docs: 表示只修改了文档
- style: 表示修改格式、书写错误、空格等不影响代码逻辑的操作
- refactor: 表示修改的代码不是新增功能也不是修改 bug，比如代码重构
- perf: 表示修改了提升性能的代码
- test: 表示修改了测试代码
- build: 表示修改了编译配置文件
- chore: 无 src 或 test 的操作
- revert: 回滚操作

`[可选的作用域]`: 是为了描述 此次 commit 影响的范围，比如: route, component, utils, build, api, website, docs

`<描述>`: 此次提交的简短描述

`[可选的正文]`: 此次提交的详细描述，描述为什么修改，做了什么样的修改，以及开发的思路等等，输入 `\n` 换行

`[可选的页脚]`: 主要写下面2种

- Breaking changes: 在可选的正文或脚注的起始位置带有 BREAKING CHANGE: 的提交，表示引入了破坏性变更（这和语义化版本中的 MAJOR 相对应）。
- Closed issues: 罗列此次提交修复的 bug，如 fixes issue #110

# Commitizen
[Commitizen](https://github.com/commitizen/cz-cli)是一个撰写合格 Commit message 的工具。


## 安装

安装命令如下：任选其一

> ```bash
> $ npm install -g commitizen       (全局安装)
> $ npm install -d commitizen       (项目安装)
> ```

然后，在项目目录里，运行下面的命令，使其支持 Angular 的 Commit message 格式。

> ```bash
> $ commitizen init cz-conventional-changelog --save --save-exact
> ```


ps: 对于`非Node项目`(java、php...)在执行上一条命令前,需要手动创建[package.json]()文件
> ```bash
> $ npm init --yes
> ```

通过如上命令生成[package.json]()文件基本格式如下：

```json
{
  "name": "demo",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www"
  }
}
```

以后，凡是用到`git commit`命令，一律改为使用`git cz`。这时，就会出现选项，用来生成符合格式的 Commit message。如图：

![git-cz](https://cdn.jsdelivr.net/gh/larscheng/myImg/blogImg/commit/GIF.gif)


## standard-version

如果你的所有 Commit 都符合 Angular 格式，那么发布新版本时， Change log 就可以用脚本自动生成

[standard-version](https://github.com/conventional-changelog/standard-version)就是生成 Change log 的工具

## 安装使用


安装命令如下：任选其一

> ```bash
> $ npm i -g standard-version       (全局安装)
> $ npm i -S standard-version       (项目安装)
> ```


生成CHANGELOG：

在[package.json]()中的`script`中 加入配置:

> "scirpt":{"release":"standard-version"}

直接执行，即可生成CHANGELOG文件
> ```bash
> $ npm run release
> ```


备注：

> 生成CHANGELOG的工具很多，[conventional-changelog-cli](https://github.com/conventional-changelog/conventional-changelog/tree/master/packages/conventional-changelog-cli)也可以用来生成CHANGELOG，安装使用方法和`standard-version`类似



本项目的CHANGELOG生成实例：[CHANGELOG查看](https://github.com/larscheng/Conventional-Commits-Demo/blob/master/CHANGELOG.md)


