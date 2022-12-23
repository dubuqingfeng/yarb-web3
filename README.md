# yarb (Yet Another Rss Bot)

来自：https://github.com/VulnTotal-Team/yarb

一个方便获取每日 web3 资讯的爬虫和推送程序。支持导入 opml 文件，因此也可以订阅其他任何 RSS 源。

**懒人福音，每日自动更新，点击右上角 Watch 即可：[每日安全资讯](./today.md)，[历史存档](./archive)**

- [yarb (Yet Another Rss Bot)](#yarb-yet-another-rss-bot)
  - [安装](#安装)
  - [运行](#运行)
    - [本地搭建](#本地搭建)
    - [Github Actions](#github-actions)
  - [订阅源](#订阅源)
  - [关注我们](#关注我们)

## 安装

```sh
$ git clone https://github.com/dubuqingfeng/yarb-web3.git
$ cd yarb && ./install.sh
```

## 运行

### 本地搭建

编辑配置文件 `config.json`，启用所需的订阅源和机器人（key 也可以通过环境变量传入），最好启用代理。

```sh
$ ./yarb.py --help                            
usage: yarb.py [-h] [--update] [--cron CRON] [--config CONFIG] [--test]
optional arguments:
  -h, --help       show this help message and exit
  --update         Update RSS config file
  --cron CRON      Execute scheduled tasks every day (eg:"11:00")
  --config CONFIG  Use specified config file
  --test           Test bot

# 单次任务
$ ./yarb.py

# 每日定时任务
$ nohup ./yarb.py --cron 11:00 > run.log 2>&1 &
```

### Github Actions

利用 Github Actions 提供的服务，你只需要 fork 本项目，在 Settings 中添加 secrets，即可完成部署。

目前支持的推送机器人及对应的 secrets：

- [邮件机器人](https://service.mail.qq.com/cgi-bin/help?subtype=1&&id=28&&no=1001256)：`MAIL_KEY`（需要申请授权码）（订阅较多时推荐）
- [飞书群机器人](https://open.feishu.cn/document/ukTMukTMukTM/ucTM5YjL3ETO24yNxkjN)：`FEISHU_KEY`
- [企业微信群机器人](https://developer.work.weixin.qq.com/document/path/91770)：`WECOM_KEY`
- [钉钉群机器人](https://open.dingtalk.com/document/robots/custom-robot-access)：`DINGTALK_KEY`
- [QQ群机器人](https://github.com/Mrs4s/go-cqhttp)：`QQ_KEY`（需要关闭登录设备锁）
- [Telegram机器人](https://core.telegram.org/bots/api): `TELEGRAM_KEY`（需要代理）

## 订阅源

推荐订阅源：

- [CustomRSS](rss/CustomRSS.opml)

其他订阅源：

- [RSSAggregatorforWeb3](https://github.com/chainfeeds/RSSAggregatorforWeb3)

添加自定义订阅有两种方法：

1. 在 `config.json` 中添加本地或远程仓库：

```json
{
  "rss": {
      "CustomRSS": {
          "enabled": true,
          "filename": "CustomRSS.opml"
      },
      "CyberSecurityRSS": {
          "enabled": true,
          "url": "https://raw.githubusercontent.com/zer0yu/CyberSecurityRSS/master/CyberSecurityRSS.opml",
          "filename": "CyberSecurityRSS.opml"
      },
```

2. 在 `rss/CustomRSS.opml` 中添加链接：

```opml
<?xml version="1.0" encoding="UTF-8"?>
<opml version="2.0">
<head><title>CustomRSS</title></head>
<body>
<outline type="rss" xmlUrl="https://forum.butian.net/Rss" text="奇安信攻防社区" title="奇安信攻防社区" htmlUrl="https://forum.butian.net" />
</body>
</opml>
```
