---
layout: layout.pug
navigationTitle:  dcos marathon group add
title: dcos marathon group add
menuWeight: 17
excerpt: Adding a Marathon group
enterprise: false
---


# Description

The `dcos marathon group add` command allows you to add a Marathon group.

# Usage

```bash
dcos marathon group add [<group-resource>]
```

# Options

| Name | Description |
|---------|-------------|
| `-h`, `--help` | Display info about usage of this command. |


## Positional arguments

| Name |  Description |
|---------|-------------|
| `<group-resource>`   | Path to a file or HTTP(S) URL that contains the group's JSON definition. If omitted, the definition is read from `stdin`. For a detailed description see the [documentation](/mesosphere/dcos/1.12/deploying-services/marathon-api/). |

# Parent command

| Command | Description |
|---------|-------------|
| [dcos marathon](/mesosphere/dcos/1.12/cli/command-reference/dcos-marathon/) | Deploy and manage applications to DC/OS. |

