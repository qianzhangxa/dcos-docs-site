---
layout: layout.pug
navigationTitle:  部署服务和 Pod
title: 部署服务和 Pod
menuWeight: 130
excerpt: 使用 Marathon 管理您的流程和服务
render: mustache
model: /mesosphere/dcos/1.13/data.yml
enterprise: false
---

DC/OS 使用 Marathon 管理流程和服务。

Marathon 是 DC/OS 的“初始化系统”。Marathon 启动和监控应用程序和服务，自动修复故障。

本地 Marathon 实例作为 DC/OS 安装的一部分进行安装。DC/OS 启动后，您可以通过带有 [`dcos marathon`](/mesosphere/dcos/cn/1.13/cli/command-reference/dcos-marathon/) 命令的 DC/OS CLI 管理本地 Marathon 实例。

DC/OS 服务是部署在 DC/OS 上的 Marathon 应用程序。DC/OS 服务可从 [Mesosphere {{ model.packageRepo }}](/mesosphere/dcos/cn/1.13/overview/concepts/#mesosphere-universe) 等包资源库获取，您也可以自己创建。

# DC/OS 服务

您可以运行您创建的 DC/OS 服务，也可以从 [{{ model.packageRepo }}](/mesosphere/dcos/cn/1.13/gui/catalog/) 中安装包。创建的服务和在 {{ model.packageRepo }} 中安装的服务在运行时都会显示在 DC/OS Web 界面的 **服务** 选项卡中。

您自己创建的服务由 Marathon 管理，可以 [在 DC/OS CLI 中](/mesosphere/dcos/cn/1.13/cli/command-reference/)（带有 `dcos marathon` 子命令（例如，`dcos marathon app add <myapp>.json`）或通过 DC/OS web 界面。

# {{ model.packageRepo }} 包资源库
Mesosphere 或社区（如 Spark 或 Kafka）创建的打包 DC/OS 服务会出现在 DC/OS Web 界面的 **{{ model.packageRepo }}** 选项卡上，或者可以在 [DC/OS CLI](/mesosphere/dcos/cn/1.13/cli/command-reference/) 中搜索包。可以通过 DC/OS Web 界面，或者通过带有 [`dcos package install <package-name>`](/mesosphere/dcos/cn/1.13/cli/command-reference/dcos-package/dcos-package-install/) 命令的 DC/OS CLI 配置和运行 {{ model.packageRepo }} 服务。
