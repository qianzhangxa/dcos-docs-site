---
layout: layout.pug
navigationTitle: 故障排除
title: 故障排除登录 
excerpt: 排除 DC/OS 中的登录问题
menuWeight: 50
---

# 排除登录问题

## Admin Router

Admin Router 将登录请求移交给 IAM。使用以下命令确认在任何管理节点上的 Admin Router 已接收到请求：

```bash
sudo journalctl -u dcos-adminrouter.service
```

## 身份和访问管理器

IAM 是颁发 DC/OS 认证令牌的唯一实体。
要排除登录问题，请使用以下命令检查管理节点上的 IAM (Bouncer)：

```bash
sudo journalctl -u dcos-bouncer.service
```
