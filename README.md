# 基于谷歌拓展的搜狗微信公众号文章爬虫

## 概述

此处使用谷歌拓展，模拟用户点击行为，自动完成 点击 - 回退动作。
并与此过程中完成数据的抓取行为。


## 使用说明
1. 加载插件
   1. 解压缩文件包 
   2. 打开chrome 浏览器，浏览器里输入  chrome://extensions/ 开启开发者模式，
   3. 点击加载已解压的拓展程序，加载刚才已解压的文件夹
2. 进入搜狗微信列表页，点击插件图表，点击弹窗中的 start
3. 开始收集
4. 点击stop停止收集
5. 点击get data 获取 JSON 格式的数据。

## 动机

搜狗微信对应微信真实公众号文章详情页的跳转URL做了加密，通过直接输入URL的方式无法跳转至详情页。
由于本工具目的仅限于小规模，低频率地获取部分微信特定主题公众号文章。

所以采用谷歌拓展工具模拟的方式。

好处在于，技术结构 & 使用都比较简单。


## 技术流程

1. 进入搜狗微信搜索列表页
2. 点击开始，首先统一列表页中当前页面的线索数，然后进行抓取，获取格式化数据，连带页码发送给后台
3. 然后依次点击链接，进入详情页，在详情页，抓取信息，发送至后台，后台在数据发送完毕1s后关闭页面
4. 针对线索逐一进行
5. 线索出栈完毕，点击下一页，执行下一波收集

由于在此过程中，由于页面一直在不停的跳转，所以实际是 background.js 在中间其调度作用。

注1：通过 iframe 的方式是无效的，搜狗屏蔽了通过 iframe 的请求
注2：由于搜狗的异常行为检测，大概每5页（50条记录）需要输入一下验证码