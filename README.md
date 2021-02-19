# 介绍

这是一个基于`Vue`开发的运行时类博客文档，不具备被搜索引擎爬取的能力，事实上，爬虫文密布的搜索引擎不能够帮助用户快速检索到内容，这会极大的浪费国家效率，因此，我痛恨爬虫，这也是为`稻壳猫`诞生的原因，逐步摆脱对搜索引擎的依赖，构建个人知识库，填补个人生活工具链空白的一部分，项目远未达到开源的水准，私用

## 工作原理

`docat`是由vue驱动，运行时的spa应用，本质上就是一个js文件，没有构建过程，你只需在`doc@`文件夹下，编写`markdown`文件，并且配置哪些`markdown`是需要展示的，例如：

```javascript
/           => index.md
/foo        => foo.md
/book/foo   => book/foo.md
```

## 类似App

- Nuxt：面向前端开发者，学习成本高，需要用户构建`node.js`环境，安装海量依赖……
- Hexo：多如牛毛的配置项，不同的主题，不同的配置项，并且，随着文件系统增多，编译时间感人
- 语雀/GitBook：弥漫商业气息
- Docsify/Docute：同样基于Vue，运行时，配置上仍略嫌麻烦

## 搜索

由于`docat`为运行时驱动，在搜索功能上，选择了本地化建立索引的方案。随之而来的便是『到底多久重建一次索引』，为了防止过度消耗服务器带宽，索引重建时间默认为`300`秒，如果是高频更新用户，可以自定义在`_app.md`中配置索引重建时间。

# 语法增强

## 代码高亮

默认使用了`highlight.js`作为解析器，支持

- `css`
- `javascript`
- `typescript`
- `bash`
- `css`
- `htmlbars`
- `xml`
- `json`
- `java`
- `less`
- `markdown`
- `sql`

要使用语法高亮，需要在代码块第一行添加对应的语言声明，eg：` ```html your code here ``` `

## 横幅

` > 常规的横幅 `,eg：

> 常规的横幅

`>!! 耀眼的横幅`,eg：

>!! 耀眼的横幅，借鉴了docsify的UI设计

`>?? 此处有疑问`

>?? 此处有疑问

# 配置gogs GIT钩子

场景：以Gogs为例，先git push `A项目` 到远程仓库 `REPO`，服务端web目录`webB`文件夹触发钩子执行 git pull

1、gogs初始化一个仓库`REPO`，仓库设置=>管理GIT钩子=>post-receive，填入

```bash
#!/bin/sh
export GIT_WORK_TREE=/www/wwwroot/webB
export GIT_DIR=${GIT_WORK_TREE}/.git
cd ${GIT_WORK_TREE}
git pull
```

2、利用ssh工具登录服务器

```bash
ssh root@mozzie.cn
```

3、生成ssh key

```bash
ssh-keygen -t rsa -C "himozzie@foxmail.com"
```

4、配置公钥到gogs

```bash
cat ~/.ssh/id_rsa.pub
```

把打印出的公钥，配置到ssh密钥

5、最后一步

配置好服务端的公钥后，就可以无需用户名密码，`cd /webB`目录下，执行`git pull`，此后每次`git push A项目`，服务端都会触发`GIT钩子`，自动从`REPO`拉取最新的仓库文件


# Changelog

## 2021年1月30日 15点52分

- fix: 目录文章滚动同步引入`debounce`机制，优化性能
- add: `> ??`横幅语法扩展

## 2021年2月4日 05点46分

- add: 增加文章阅读记录提示 5s delay

## 2021年2月5日 05点33分

- fix: 优化代码结构

## 2021年2月7日 00点43分

- fix: 优化了css
- fix: 解决了若干bug
- add: 自动跳转到上次浏览位置

## 2021年02月19日 00点42分

- add: 新增搜索功能
