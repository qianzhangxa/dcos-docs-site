---
layout: layout.pug
navigationTitle: dcos storage provider
title: dcos storage provider
menuWeight: 0
notes: Code generated by docgen.go, DO NOT EDIT
enterprise: true
beta: true
origin: github.com/mesosphere/dcos-storage/cli/pkg/cmd/cmd_provider.go
excerpt: Manage volume providers.
---
#include /dcos/services/include/beta-software-warning.tmpl

## dcos storage provider

Manage volume providers.

### Synopsis

A volume provider manages storage capacity offered by a CSI plugin to the DC/OS
cluster through a DC/OS Storage Plugin. A DC/OS Storage Plugin consists of a CSI
plugin along with some glue that integrates it into DC/OS. A volume provider
that specifies its plugin as `lvm` is referred to as an "lvm" volume provider.

There are two kinds of volume provider:

1. Local volume provider - A local volume provider manages storage capacity that
is tied to a specific Mesos agent, such as an LVM2 volume group managed by an
"lvm" volume provider.

2. External volume provider - An external volume provider manages storage
capacity that is not tied to any specific Mesos agent, such as a volume
provider, which uses the Amazon EBS API to remotely operate on any Mesos agent
in the cluster.

There can be several volume providers for the same type of CSI plugin. For
example: each LVM2 CSI plugin manages a single LVM2 volume group (VG), and when
there are multiple LVM2 volume groups on an agent each LVM2 volume group will be
configured as a separate volume provider.

```bash
dcos storage provider [flags]
```

### Options inherited from parent commands

Name | Description
--- | ---
`-h`,`--help` | Help for this command.
`--timeout` duration | Override the default request timeout. (default 55s)
