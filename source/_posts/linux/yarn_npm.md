title: yarn_npm
draft: true
categories:
  - linux
tags: [yarn npm]
date: 2021-07-10 00:00:00
---


{% codeblock "commands" lang:sh %}
yarn config set registry 'https://registry.npm.taobao.org'
yarn config get registry

yarn global add yrm
yrm ls
yrm use taobao
yrm test

npm config set registry https://registry.npm.taobao.org
npm config get registry
{% endcodeblock %}
