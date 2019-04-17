---
published:  ture
layout:     post
title:      "远程访问Hass"
date:       2019-04-17
author:     "SchumyHao"
tags:
  - homeassistant
  - molohub
  - 远程访问
---

## 为什么要外网访问Hass?

----
开始使用Homeassistant的时候, 特别看重的是它的服务部署在本地局域网内, **安全**, **稳定**, **靠谱**!  
但是现实是很少有智能单品提供单一局域网内的服务, 所以一味地强调局域网=安全, 有点[房间里的大象](https://zh.wikipedia.org/zh-cn/%E6%88%BF%E9%96%93%E8%A3%8F%E7%9A%84%E5%A4%A7%E8%B1%A1)的意思了.  

*下班前提前启动洗衣机*, *放假回老家后定期观察一下家里状况*, *提示可疑人员在总在家门口徘徊*.  

**这些都是刚需**, 我们不应该否认这件事.

## 谨记

----

1. 任何外网访问都有可能存在安全风险, 请使能Hass的[MFA](https://www.home-assistant.io/docs/authentication/multi-factor-auth/)功能.
2. 请个人自行权衡外网访问风险性和便利性之间的自己更看重哪方面.

## molohub

----
### 介绍
[molohub](https://www.molo.cn/)是一款给大家提供外网访问Hass的免费(至少一年)工具.  
受限于绝大多数家庭的网络都没有外网访问需要的外网IP和个人域名, 所以之前要想实现外网访问Hass, 用户需要至少拥有一个自己的VPS和域名, 在VPS和局域网内搭建内网穿透服务(FRP或ngrok). 搭建对技术要求很高, 搭建**稳定**的系统对技术要求更高, 搭建**稳定**且**安全**的系统那必须要把自己逼成大神了.  
molohub工具为大家搭建了完整的内网穿透服务, 而且用户端可以选择使用**微信小程序**在移动端轻松远程访问, 也可以使用github账号登录, 在PC web端远程访问家里的Hass.

### 安装

![installmolohub2](/img/in-post/2019-04-17-Hass外网访问服务的工具__molohub/install.gif)

molohub是以hass component的形式呈现的, 并且没有第三方的python module的依赖, 所以对于直接pip安装hass, hassbain, hassio都可以方便使用.  
1. 从项目[github](https://github.com/haoctopus/molohub)页面上下载项目源码压缩包并解压.
2. 将molohub源码拷贝到Homeassistant配置路径下的custom_components文件夹下.
3. 检查Hass配置并重新启动Hass服务(主要针对Hassio配置检查的机制)
4. 在configuration.yaml中添加molohub
```yaml
molohub:
```
5. 检查Hass配置并重新启动Hass服务.
6. 在Hass页面上选择适合于自己的外网接入方式并绑定.

### 多账户绑定

![multimolohub2](/img/in-post/2019-04-17-Hass外网访问服务的工具__molohub/oAuth.gif)

如果要多个账户绑定一个hass, 实现家人共同访问或自己多平台访问, 需要一些小技巧.  
1. 将custom_components路径下的molohub代码复制一份并且给一个新的独一无二的文件夹名字.
2. 在configuration.yaml中添加这个新molohub代码文件夹的名字.
3. 重启Hass服务后, 会多一个绑定的通知框, 再绑定即可.

### 官方承诺

![offical](/img/in-post/2019-04-17-Hass外网访问服务的工具__molohub/offical.png)

1. 全部使用https方式访问, 保证网络传输过程中的安全性.
2. 至少1年免费使用.

## 结束

----

信任是双方长期建立关系, 根据个人的角色, 性格, 需求等因素综合考虑是否合适使用molohub.