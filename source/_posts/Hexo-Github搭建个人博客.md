---
title: Hexo+Github搭建个人博客
date: 2025-04-06 15:54:47
tags: 博客搭建
categories: 博客搭建教程
comments: true
---

## 前言
笔者认为，搭建个人博客不仅可以帮助自己梳理所学的知识，还可以为其他正在学习的伙伴提供参考，所以大家都可以尝试搭建一个属于自己的个人博客，时常以博客的形式总结、分享自己的学习心得。本文将介绍如何使用**Hexo+Github**搭建个人博客。

PS：该方法适用于有一定 *git* 使用基础的人，且在后续博客编写发布流程中需要有一定的 *Markdown* 基础。

## 开始搭建
### 安装 Hexo
Hexo是基于Node.js的静态博客网站生成器，所以在安装Hexo前我们需要先安装Node.js，可以直接从[官网下载](https://nodejs.org/zh-cn/download)，Windows用户推荐使用官方的Installer工具(.msi)下载安装。

安装完成后，打开命令行，输入以下命令，若出现版本号则说明安装成功：
```bash
node -v
npm -v
```

安装Hexo，在命令行输入以下命令：
```bash
npm install -g hexo-cli
```

### 创建博客
安装完成之后，创建一个用于存放博客文件的文件夹，比如命名为 *myblog*，然后进入该文件夹，在该文件夹下打开命令行，输入以下命令：
```bash
hexo init
```

如果看到如下信息，说明初始化成功：
```bash
INFO  Cloning hexo-starter https://github.com/hexojs/hexo-starter.git
INFO  Install dependencies
# 一些可能的中间信息
INFO  Start blogging with Hexo!
```

接着安装需要的依赖：
```bash
npm install
```

### 博客目录介绍
下面是初始化后的博客目录结构，红框标记出的是比较重要的文件和子目录：
{% image /images/hexo-github博客搭建/hexo目录结构.jpg %}
- **_config.yml**：博客的配置文件，包括博客标题、作者、主题、插件等配置。
- **source/**：存放博客文章的文件夹，文章以.md为后缀名。
- **themes/**：存放博客主题的文件夹，默认主题为landscape。
- **scaffolds/**：存放博客文章模板的文件夹，默认有三种模板：post、page、draft，可根据个人偏好进行个性化配置。

### 本地预览
在博客文件夹下打开命令行，输入以下命令：
```bash
hexo s
```

如果看到如下信息，说明本地预览启动成功：
```bash
INFO  Validating config
INFO  Start processing
INFO  Hexo is running at http://localhost:4000/ . Press Ctrl+C to stop.
```

打开浏览器，输入 *http://localhost:4000*，即可看到博客的预览效果。
{% image /images/hexo-github博客搭建/hexo本地预览.jpg %}

### 生成新文章
在博客文件夹下打开命令行，输入以下命令：
```bash
hexo new "文章标题" # 随便起一个喜欢的标题
```

这时，在 `source/_posts/` 目录下会生成`文章标题.md`文件，这就是你的第一篇博客文章了。

执行以下命令，将文章生成为静态网页：
```bash
hexo g
```

再次本地预览时，就可以看到新发布的文章了。
{% image /images/hexo-github博客搭建/hexo生成新文章.jpg %}

### 部署到Github
首先，你需要一个Github账号，如果没有的话，需要先注册一个。（Github访问有困难的小伙伴，这里笔者推荐[Watt Toolkit](https://steampp.net/download)对Github进行加速，就可以正常访问了。）然后，创建一个仓库，仓库名称必须为`用户名.github.io`，比如我的仓库名称就是`Apricity12138.github.io`。
{% image /images/hexo-github博客搭建/github仓库创建.jpg %}

接着，在博客目录打开Git Bash创建本地git仓库（如果没有git，则需要[下载git](https://git-scm.com/downloads)，配置说明），并将其推送至远程Github仓库（[第一次使用的配置教程](https://blog.csdn.net/m0_68987050/article/details/146215006)）：
```bash
git init
git add .
git commit -m "my blog first commit"
git remote add origin "远端github仓库地址"
git branch -M main
git push -u origin main
```

成功推送到远程仓库之后，找到博客目录下的`_config.yml`文件，修改以下内容：
```yml
# 这段内容通常在_config.yml文件的最下方
deploy:
  type: git
  repo: # 远端 Github 仓库地址
  # 请修改为你的远程仓库的主分支名称，如果你按照上面的步骤操作，则分支名为main
  # Github 仓库分支名一般在仓库文件列表的左上角
  branch: main
```

安装git部署依赖插件：
```bash
npm install hexo-deployer-git --save
```

然后执行以下命令，将博客部署到Github（每次在本地添加、删除或修改文章后，都需要执行）：
```bash
hexo g
hexo d
```

最后，在浏览器中键入`用户名.github.io`，即可访问你的博客了。（如果遇到网络问题无法加载，请尝试开启 Watt Toolkit 的 Github 加速。）

## 结语
至此，你已经成功搭建了自己的个人博客，接下来就可以尽情地写博客了。当然，博客的搭建还有很多细节和技巧，比如更换主题、添加插件、自定义域名等，这里就不一一介绍了，有兴趣的小伙伴可以自行探索。如果需要的话，各位小伙伴可以在评论区留言，笔者会尽力解答，谢谢大家的支持！
