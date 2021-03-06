---
layout: layout.pug
navigationTitle:  创建密钥
title: 创建密钥
menuWeight: 1
excerpt: 使用键值对或文件创建密钥
enterprise: true
render: mustache
model: /mesosphere/dcos/2.0/data.yml
---


您可以使用键值对或作为文件在 DC/OS 中创建密钥。两种方法都将名称和密钥值添加到密钥存储库中。如果您已将密钥值存储在本地文件中，并希望避免复制和粘贴，那么您可能会发现将密钥添加为文件会很方便。

有关如何在应用程序或 pod 定义中引用这些密钥的信息，请参阅[配置服务和 pod 以使用密钥](/mesosphere/dcos/cn/2.0/security/ent/secrets/use-secrets/)。

<p class="message--important"><strong>重要信息：</strong>密钥的最大文件大小约为 1 MB，减去了大约 1 KB 的密钥存储库元数据。</p>


# 创建密钥

以下部分解释了如何使用 UI、CLI 和密钥 API，将密钥创建为键/值对和文件。

密钥应包括路径，除非您希望允许所有服务访问其值。有关密钥路径的更多信息，请参阅[空间](/mesosphere/dcos/cn/2.0/security/ent/#spaces)。

## 前提条件

### DC/OS UI
- `dcos:superuser` 权限。

### DC/OS CLI 或密钥 API

- 有关从 CLI 或 API 创建密钥所需的权限，请参阅[密钥存储库权限](/mesosphere/dcos/cn/2.0/security/ent/perms-reference/#secrets)。您配置的权限必须包括允许用户创建的密钥名称。每个密钥必须拥有一项权限。密钥名称和权限名称必须匹配。

- [已安装 DC/OS CLI](/mesosphere/dcos/cn/2.0/cli/install/) 以及 [已安装 DC/OS Enterprise CLI](/mesosphere/dcos/cn/2.0/cli/enterprise-cli/#ent-cli-install)。

# <a name="ui"></a>使用 UI 创建键值对密钥

1. 以具有 `dcos:superuser` 权限的用户身份登录 DC/OS UI。

1. 打开 **Secrets** 选项卡。

1. 单击右上方的 **+** 图标。

    ![新密钥](/mesosphere/dcos/2.0/img/new-secret.png)

    图 1 - 新密钥图标

    如果您当前没有密钥，将显示 **创建密钥** 界面。单击 **创建密匙** 按钮。

    ![创建密钥](/2.0/img/GUI-Secrets-Create-Secret.png)

    图 2 -“创建密匙”按钮

1. 在 **创建新密钥** 屏幕的 **ID** 框中，键入密钥的名称及其路径（若有）。

    ![密钥 ID 键对](/2.0/img/GUI-Secrets-Create-New-Keypair.png)

    图 3 - 创建新的键对 

1. 选择 **键值对** 作为类型。

1. 在 **Value** 框中键入或粘贴密钥。
    ![密钥 ID/值字段](/2.0/img/GUI-Secrets-Create-New-Keypair.png)

    图 4 - 创建新密钥

1. 单击 **创建密匙**。

返回到“密匙”屏幕，您可以看到密匙已经部署。

   ![已部署密匙](/mesosphere/dcos/2.0/img/GUI-Secrets-Secrets-Keypair-Deployed.png)

   图 5 - 部署了键对的密钥

# <a name="api"></a>使用 API 创建键值对密钥

本程序介绍了如何在 `developer` 路径内创建名为 `my-secret` 的密钥。

<p class="message--note"><strong>注意：</strong>在发出本部分中的 curl 命令之前，必须遵循 <a href="/mesosphere/dcos/cn/2.0/security/ent/tls-ssl/get-cert/">获取 DC/OS CA 捆绑包</a> 中的步骤。</p>


1. 使用 `dcos auth login` 登录到 CLI。

1. 使用以下命令创建密钥。

   ```bash
   curl -X PUT --cacert dcos-ca.crt -H "Authorization: token=$(dcos config show core.dcos_acs_token)" -d '{"value":"very-secret"}' $(dcos config show core.dcos_url)/secrets/v1/secret/default/developer/my-secret -H 'Content-Type: application/json'
   ```

# <a name="cli"></a>通过 DC/OS Enterprise CLI 创建键/值对密钥

本程序介绍了如何使用 DC/OS Enterprise CLI 在 `developer` 路径内创建名为 `my-secret` 的键/值对密钥。

1. 使用 `dcos auth login` 登录到 CLI。您可在 [CLI 参考](/mesosphere/dcos/cn/2.0/cli/command-reference/dcos-auth/dcos-auth-login/) 中找到有关此命令的更多信息。

1. 使用以下命令创建新密钥。

   ```bash
   dcos security secrets create --value=top-secret developer/my-secret
   ```
   

# 通过 DC/OS Enterprise CLI 从文件创建密钥

本程序介绍了如何使用文件在 `developer` 路径内使用 DC/OS Enterprise CLI 创建名为 `my-secret` 的密钥。

文件内容（以下称为 `my-secret.txt`）可以是任何文本值。

<p class="message--note"><strong>注意：</strong>从 DC/OS 1.10 开始，您只能从 DC/OS CLI 上传密钥作为文件。密钥的最大文件大小约为 1 MiB，减去了密钥存储库元数据的大约 1 KB。</p>

1. 使用 `dcos auth login` 登录到 CLI。您可在 [CLI 参考](/mesosphere/dcos/cn/2.0/cli/command-reference/dcos-auth/dcos-auth-login/) 中找到有关此命令的更多信息。

1. 使用以下命令创建新密钥。

  ```bash
  dcos security secrets create -f my-secret.txt developer/my-secret
  ```

  <p class="message--important"><strong>重要信息：</strong>密钥的最大文件大小约为 1 MB，减去了密钥存储库元数据的大约 1 KB。</p>

# 通过 DC/OS UI 从文件创建密钥

本程序介绍如何通过 DC/OS Web 界面使用文件来创建密匙。

1. 以具有 `dcos:superuser` 权限的用户身份登录 DC/OS UI。
1. 单击左侧导航菜单上的 **密匙** 选项卡。
1. 单击右上方的 **+** 图标。

    ![新密钥](/mesosphere/dcos/2.0/img/new-secret.png)

    图 6 -“密匙”屏幕

    如果您当前没有密钥，将显示“创建密钥”屏幕。单击 **创建密匙** 按钮。

    ![创建密钥](/mesosphere/dcos/2.0/img/GUI-Secrets-Create-Secret.png)

    图 7 -“创建密匙”按钮

1. 在 **ID** 框中，提供密钥名称及其路径（如果有）。

    ![创建新密钥](/mesosphere/dcos/2.0/img/GUI-Secrets-Create-New-Secret.png)

    图 8 - 显示选定文件的“创建新密钥”对话框

1. 选择 **文件** 作为类型。
1. 单击 **选择文件**。
1. 找到并选择要据其创建密匙的文件。
1. 单击 **创建密匙**。

返回到“密匙”屏幕，您可以看到密匙已经部署。

   ![已部署密匙](/mesosphere/dcos/2.0/img/GUI-Secrets-Deployed.jpeg)

   图 9 -  部署的密钥
