---
title: Hexo
date: 2022-01-09
category: Command
---
<!--more-->
# Hexo

## 1. 安装 NodeJs
windows/mac 安装

[NodeJs官网](https://nodejs.org/en/download/)

检查是否安装成功
```bash
node -v
```

npm 换源
```shell
npm config set registry https://registry.npmmirror.com/
```

检测是否修改成功
```shell
npm config get registry
```

## 2. 安装 Hexo
安装命令，如果太久没用版本会过低，需要更新 `package-lock.json`
```shell
npm install hexo-cli -g
```

检查是否安装成功
```shell
hexo -v
```

初始化文件夹
```shell
hexo init blog
```

## 3. 安装相关支持库

git 支持
```shell
npm install hexo-deployer-git --save
```
search 支持
```shell
npm install hexo-generator-feed --save
```

## 4. 公式相关依赖
```shell
npm uninstall hexo-renderer-marked --save
```
```shell
npm install hexo-renderer-kramed --save
```

打开node_modules/hexo-renderer-kramed/lib/renderer.js，将

```javascript
// Change inline math rule
function formatText(text) {
    // Fit kramed's rule: $$ + \1 + $$
    return text.replace(/`\$(.*?)\$`/g, '$$$$$1$$$$');
}
```
改为
```javascript
// Change inline math rule
function formatText(text) {
    return text;
}
```

```shell
npm uninstall hexo-math --save
```
```shell
npm install hexo-renderer-mathjax --save
```

打开node_modules/hexo-renderer-mathjax/mathjax.html，最后一行改为
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.1/MathJax.js?config=TeX-MML-AM_CHTML"></script>
```

打开node_modules/kramed/lib/rules/inline.js:

将
```javascript
escape: /^\\([\\`*{}\[\]()#$+\-.!_>])/,
```
改为
```javascript
escape: /^\\([`*\[\]()# +\-.!_>])/,
```

将
```javascript
em: /^\b_((?:__|[\s\S])+?)_\b|^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
```
改为
```javascript
em: /^\*((?:\*\*|[\s\S])+?)\*(?!\*)/,
```

在home/_config.yml，中添加如下内容
```yml
mathjax:
    enable: true
```

## 使用
```bash
hexo clean && hexo generate && hexo server -p 4001
hexo deploy
```

## 参考
> [1. 在HEXO主题中添加数学公式支持 ](https://www.cnblogs.com/zhyantao/p/10424874.html)
> [2. highlight.js](https://highlightjs.org/#usage)
> [3. 文档 | Hexo](https://hexo.io/zh-cn/docs/)

