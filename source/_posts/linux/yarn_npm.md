title: yarn_npm
draft: true
categories:
  - linux
tags:
  - yarn npm
date: 2021-07-10 00:00:00
---
## yarn/npm 设置国内源


### 临时
```sh
npm --registry https://registry.npm.taobao.org install express
```

### 写入文件

#### command
```sh
yarn config set registry 'https://registry.npm.taobao.org'
yarn config get registry

npm config set registry https://registry.npm.taobao.org
npm config get registry
```

#### use yrm
```sh
npm install -g yrm
# yarn global add yrm
yrm ls
yrm use taobao
yrm test
```
