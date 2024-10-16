---
title: 使用SSHFS将Linux目录挂载为Windows磁盘
published: 2024-10-12
description: 'SSHFS拥有图形界面，可以通过SFTP协议将Linux目录映射为一个本地磁盘，便于管理文件'
image: './assets/images/QmZZkpG3gkkQjGExXvG9vbuAJyBfHGWEFH2Bk8YzhSSqwx.webp'
tags: [SSHFS]
category: '实用工具'
draft: false 
lang: ''
---

### 有一款更好用的软件，支持多达42种服务或协议：[RaiDrive](https://onani.cn/RaiDrive)😋

---

### 优点

可以像管理Windows文件一样管理Linux文件，不需要敲代码

---

### 正式开始

1. 下载并安装下面的软件

::github{repo="billziss-gh/sshfs-win"}

::github{repo="billziss-gh/winfsp"}

::github{repo="evsar3/sshfs-win-manager"}

2. 打开SSHFS-Win Manager，添加你的SSH服务器（我这里使用私钥连接）
   ![QmccEuSGovyVuJeTRYEUKNr2XSPpKTeoqq82rZYMyhazh2.png](assets/images/ff6462dca9c79a35f3a5b7816d997396d6f2accf.png)

3. 点击连接即可将Linux目录挂载到本地磁盘
   ![QmQHZCeYbQ3GmjWDqWqEpdXWYnQy6KHnep5m6bu6X3eCNH.png](assets/images/9f6796b969af0b43136fc44a2773f2a2baa06006.png)

4. 效果
   
   ![QmNjTfv6XncV2dVddt4k6E9XN6tjuXf5rmXPhh2ggcemkU.png](assets/images/add85483f97c229cee0a53f8cae7d7957b5d7d9c.png)
   
   ![QmWMQHNpJUUPg9B1Hdw2zmwLx9q6bcS52nUFiB3P9iYvU9.png](assets/images/d4ec6f87893f4af5d7eedb2e2a19a784fd6c6f92.png)

### 疑难解答

如果无法连接，请打开设置的Debug Panel，根据报错着手解决
![image](https://ipfs.crossbell.io/ipfs/QmWW58e68YLKFoKbZG63CwWVqgxkGfDiCJrM42Hj9hcN6M?img-quality=75&img-format=auto&img-onerror=redirect&img-width=3840)

![QmWW58e68YLKFoKbZG63CwWVqgxkGfDiCJrM42Hj9hcN6M.png](assets/images/f86e715e2b925d251c346d42b0f9bb1c3481ba7b.png)
