---
title: hexo常用指令集
date: 2026-05-02 18:02:12
tags:
---
1. 核心创作指令
当你有了灵感，想写新内容时：

hexo n "文章标题"：新建文章。这里的 n 是 new 的缩写。

会在 source/_posts 目录下生成一个 .md 文件。

hexo n page "页面名"：新建页面（比如“关于我”或“留言板”）。

2. 本地预览（最常用）
在把文章发到网上之前，你肯定想先看看长啥样：

hexo s：启动本地服务器预览。s 是 server 的缩写。

启动后访问 http://localhost:4000 即可查看。

提示：在刚才的 PowerShell 报错解决后，这个命令就可以直接用了。

3. 清理与生成（发布前必做）
当你要更新博客到线上时，建议走一遍这套“三部曲”：

hexo clean：清理缓存文件（db.json）和生成的静态网页（public 文件夹）。

如果你修改了主题配置或发现网页没更新，执行这个准没错。

hexo g：生成静态文件。g 是 generate 的缩写。

把你的 Markdown 文章转换成浏览器能看懂的 HTML 网页。

hexo d：部署到线上。d 是 deploy 的缩写。

自动把生成的网页上传到 GitHub Pages 或服务器。

小技巧：连招组合
你可以直接输入 hexo clean && hexo g && hexo d，这样它会自动按顺序跑完整个流程，你只需喝杯咖啡等它传完就行。

4. 其他进阶指令
hexo v：查看版本信息（version）。

hexo help：查看帮助文档。

hexo s -p 5000：如果 4000 端口被占用了，可以用这个改到 5000 端口预览。

💡 独家建议
如果你嫌每次输入 hexo generate 这种长单词太累，Hexo 的缩写规则非常一致：

g = generate

s = server

d = deploy

n = new
---
