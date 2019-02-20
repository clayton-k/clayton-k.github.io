---
title: Hexo笔记
date: 2019-02-20 21:05:26
tags: 笔记
---

#### 记录一下Hexo+Github的使用，免得隔几天重装电脑或者换个系统就又忘了怎么用Hexo

### 安装以下这两个软件

* [Node.js](https://nodejs.org/)
* [Git](https://git-scm.com/)

### 配置github

* 创建一个repository name是 "username.github.io"的仓库，如clayton-k.github.io
* GitHub Pages里配置 Custom domain，默认domain是上面的repository name，如果有自己买了域名，就改成自己买的那个域名
* [可选]勾选Enforce HTTPS 
* [其他]User pages must be built from the master branch.所以不需要选分支

### 安装Hexo(cmd或者power shell下执行)

`npm install -g hexo-cli`

### 初始化
```
hexo init <folder>
cd <folder>
npm install
```

### 体验

`hexo server`

### Hexo与Github关联
```
git config --global user.name "your user name"
git config --global user.email "your email address"
ssh-keygen -t rsa -C "your email address"
cd ~/.ssh
```

* 拷贝id_rsa.pub里面的内容到Github->Personal settings->SSH and GPG keys里，然后测试rsa密钥是否生效
`ssh -T git@github.com`
* 配置_config.yml中deploy中如下部分
```
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: git@github.com:clayton-k/clayton-k.github.io.git
  branch: master
```

* 配置本地HEXO初始化目录下的文件<folder>/source/CNAME，里面修改成自己的域名，如www.clayton-k.xyz
* 此时HEXO的命令 `hexo deploy -g` 就已经可以使用，执行该命令时，hexo会先在本地渲染好静态网页，然后通过已配置好连接的git向GitHub Pages里配置的repository branch推送变更内容，然后我们就可以从网页端访问自己的域名www.clayton-k.xyz或者github默认域名clayton-k.github.io来访问我们发布的文章

### 恢复
 * 本地HEXO初始化目录下文件的保存，可以在HEXO仓库里创建一个HEXO的分支，以供保留本地源代码，以后切换电脑的时候，只需要安装环境，然后从git上把HEXO分支clone下来，然后在clone下来的目录下执行 `npm install` 命令，就可以恢复创作的环境。