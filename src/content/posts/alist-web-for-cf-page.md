---
title: 教你把AList的前端部署到CF Pages！让你的AList秒加载！
published: 2024-10-15
description: '将AList Web部署到CF Pages可以显著提升访问者的浏览体验，因为静态资源都在CF的边缘节点，而后端使用API交互，而不是由源服务器路由所有流量，既能减轻源服务器的负载，又能使用CF Pages的不回源优势，一箭双雕'
image: './assets/images/QmSmcktDEJaWdDvFQeuNTJ9ps8R3PcLWyhSrbxoLEq2b2x.webp'
tags: [AList, Cloudflare Pages]
category: '运维'
draft: false 
lang: ''
---

## 前情提要[#](https://afo.im/shen-me-Cloudflare-dai-li-AList-tai-man--jiao-ni-bu-shu-qian-duan-dao-Pages-ju-jue-hui-yuan-#user-content-%E5%89%8D%E6%83%85%E6%8F%90%E8%A6%81)

本教程**不是 AList 的无服务器部署**，仅将前端页面部署到 Cloudflare Pages，这样用户就能很快从 cf 的边缘节点拉取前端文件，而不用 cf 回源，提高浏览体验，后端仍然需要一台开放到公网的服务器部署 AList（无公网服务器可使用 Cloudflare Tunnels）

### 首先，保证你的后端服务器支持v4v6双栈访问

1. 使用Cloudflare Tunnel，套cf

2. 分别设置A和AAAA解析，麻烦，如果你的IP很快，那其实可以不用前后端分离，暴露源站的前后端分离也不能避免被DDoS，因为你的源站会在HTTP报文中暴露

### 然后，开始正式将AList前端部署到Cloudflare Pages

1. Fork仓库：
   
   ::github{repo="alist-org/alist-web"}
2. 更改项目根目录的`env.production`文件为你的后端服务器地址  
   ![image](https://ipfs.crossbell.io/ipfs/QmduQJq3TydzvLzBn47zLxp2MR1iD2sxm67EzFUFuEBvQa?img-quality=75&img-format=auto&img-onerror=redirect&img-width=1920)
3. 将仓库克隆到本地，需要安装[Git](https://git-scm.com/)：

```
使用SSH（需要持有你的Github SSH私钥）：
git clone git@github.com:你的用户名/你Fork的仓库

使用HTTPS（Not Use Magic有概率SSL握手失败）：
git clone git@github.com:你的用户名/你Fork的仓库
```

5. 下载汉化包：[AcoFork 的网盘](https://alist.onani.cn/guest/alist_Zh-CN)或[Crowdin - 需要登录](https://crowdin.com/project/alist/zh-CN)  
   ![image](https://ipfs.crossbell.io/ipfs/QmXVpMc7BqbXv9EaAbeptsrnhYLinvQQsu1btBE3VvDixa?img-quality=75&img-format=auto&img-onerror=redirect&img-width=1080)
6. 解压，将`alist (zh-CN)\src\lang`里面的`Zh-CN`文件夹复制到仓库下`src/lang`下
7. 编辑根目录的`.gitignore`，添加一行`!/src/lang/zh-CN/`确保文件不被忽略
8. 下载[Nodejs](https://nodejs.org/zh-cn)。在根目录打开终端，生成中文需要的文件：

```
安装cnpm：
npm install -g cnpm --registry=https://registry.npmmirror.com

安装依赖：
cnpm install --legacy-peer-deps

生成中文需要的文件：
node .\scripts\i18n.mjs
```

9. 将更改提交到暂存区并提交到远程仓库，在根目录打开终端

```
git add .   //将更改提交到暂存区
git commit -m 添加中文   //发布提交
git push -f   //强制将更改提交到远程仓库
```

10. 进入[Cloudflare 仪表盘](https://dash.cloudflare.com/)，进入 Workers 和 Pages 页面  
    ![image](https://ipfs.crossbell.io/ipfs/QmW5UaUap8T2R37u5dzmKGLmUgk4qKnSMFwHBVHqvVbkVA?img-quality=75&img-format=auto&img-onerror=redirect&img-width=3840)
11. 创建一个 Pages，选择连接 Git 存储库  
    ![image](https://ipfs.crossbell.io/ipfs/QmZXerKv9PVxxscAe4w4LEfAaKfiScPQEKh1UroXnCeAUr?img-quality=75&img-format=auto&img-onerror=redirect&img-width=3840)
12. 选择你的存储库，开始设置  
    ![image](https://ipfs.crossbell.io/ipfs/QmNdSGQrJtoqDnBx8pgDrtcfmUUfVBS9xdrN4xLgyPjyXE?img-quality=75&img-format=auto&img-onerror=redirect&img-width=3840)
13. 构建命令输入：`pnpm install && pnpm build`，构建输出目录选择`/dist`  
    ![image](https://ipfs.crossbell.io/ipfs/QmbhPdbE8f1zLKvWA6aEGJtZhmecRMVZiQbx6Zx1Lecp7J?img-quality=75&img-format=auto&img-onerror=redirect&img-width=1920)
14. 等待 Cloudflare 构建结束，为 Pages 绑定自定义域  
    ![image](https://ipfs.crossbell.io/ipfs/QmTMphu61uUF9XefBAVDVf19Jm1vLVUhhXQ9PXABy7hUpK?img-quality=75&img-format=auto&img-onerror=redirect&img-width=3840)
15. 访问自定义域，查看 AList 是否正常  
    ![image](https://ipfs.crossbell.io/ipfs/QmT8GLcaxtabhifKNL8kczEtozmNvdyhzJ823RfBrcFdpm?img-quality=75&img-format=auto&img-onerror=redirect&img-width=3840)

### 定制 AList[#](https://afo.im/shen-me-Cloudflare-dai-li-AList-tai-man--jiao-ni-bu-shu-qian-duan-dao-Pages-ju-jue-hui-yuan-#user-content-%E5%AE%9A%E5%88%B6-alist)

> 我们都知道 AList 支持自定义头部和内容，但是因为 Cloudflare Pages 是一个静态页面，所以我们采用硬编码方式，直接将需要自定义的内容写入仓库根目录的`index.html`  
> ![68f1ae48204ef6e12f32ed1c8c47afdd](https://ipfs.crossbell.io/ipfs/Qmd47pgFsyh28NjhkLiCPPbf7iasXMWvAvZDupH8QspG64?img-quality=75&img-format=auto&img-onerror=redirect&img-width=2048)

1. 编辑根目录的`index.html`
2. 将更改提交到暂存区并提交到远程仓库，在根目录打开终端

```
git add .   //将更改提交到暂存区
git commit -m 你的提交摘要   //发布提交
git push -f   //强制将更改提交到远程仓库
```

3. Cloudflare Pages 会自动重新构建，等待新网页构建完成即可  
   ![ab690f2fb4494ee6505d541d5ba7a20f](https://ipfs.crossbell.io/ipfs/QmNZemsDHz5QLxW3V2eANghmVkfBccEpe5vMAWUCLik4o6?img-quality=75&img-format=auto&img-onerror=redirect&img-width=3840)
