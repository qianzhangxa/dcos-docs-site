---
layout: layout.pug
navigationTitle:  基于身份提供程序的身份认证
title: 基于身份提供程序的身份认证
menuWeight: 70
excerpt: 配置基于身份提供程序的身份认证
enterprise: true
render: mustache
model: /mesosphere/dcos/2.0/data.yml
---
<!-- The source repository for this topic is https://github.com/dcos/dcos-docs-site -->

要在组织中提供单点登录 (SSO)，您可以配置 DC/OS Enterprise 来针对一个或多个外部用户身份提供程序 (Idp) 对用户进行身份认证。相比基于目录的认证，基于身份提供程序的认证不是那么丰富（可用的信息较少），但对个人用户而言更灵活。

当用户尝试从 DC/OS Web 界面登录时，将向它们显示您已配置的第三方身份提供程序的列表。他们可以单击他们拥有 SSO 帐户的那个。

- 要搜索已配置的 IdP 的名称，请使用 `dcos auth list-providers` 命令：

    ```shell
    dcos auth list-providers
    ```
- 要搜索已配置的 IdP 的名称，请使用 `dcos auth login --provider=<provider-name> --username=<user-email> --password=<secret-password` 命令，以使用 IdP 登录。

    ```shell
    dcos auth login --provider=<provider-name> --username=<user-email> --password=<secret-password
    ```


DC/OS Enterprise 支持两种基于身份提供程序的身份认证方法：[安全声明标记语言 (SAML)](https://wiki.oasis-open.org/security/FrontPage) 和 [OpenID Connect (OIDC)](http://openid.net/connect/)：

- 添加 [SAML 身份提供程序](/mesosphere/dcos/cn/2.0/security/ent/sso/setup-saml/)
- 添加 [OpenID 身份提供程序](/mesosphere/dcos/cn/2.0/security/ent/sso/setup-openid/)：
