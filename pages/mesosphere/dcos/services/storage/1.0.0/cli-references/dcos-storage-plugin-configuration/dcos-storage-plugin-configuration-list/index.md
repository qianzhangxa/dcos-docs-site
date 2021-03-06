---
layout: layout.pug
navigationTitle: dcos storage plugin-configuration list
title: dcos storage plugin-configuration list
menuWeight: 0
notes: Code generated by docgen.go, DO NOT EDIT
enterprise: true
origin: github.com/mesosphere/dcos-storage/cli/pkg/cmd/cmd_pluginconfiguration_list.go
excerpt: Display a list of plugin configurations.
---

## dcos storage plugin-configuration list

Display a list of plugin configurations.

### Synopsis



Display a list of plugin configurations.

```bash
dcos storage plugin-configuration list [flags]
```

### Examples

1. List all plugin configurations:

```bash
dcos storage plugin-configuration list
```
```
NAME     VERSION  CREATED
devices  2        2019-01-13 13:00:00 +0000 UTC
lvm      2        2019-01-13 13:00:00 +0000 UTC
```

2. List the configuration of the LVM plugin:

```bash
dcos storage plugin-configuration list --name lvm
```
```
NAME  VERSION  CREATED
lvm   2        2019-01-13 13:00:00 +0000 UTC
```

3. List all versions of the configuration of the LVM plugin:

```bash
dcos storage plugin-configuration list --name lvm --all-versions
```
```
NAME  VERSION  CREATED
lvm   1        2019-01-12 13:00:00 +0000 UTC
lvm   2        2019-01-13 13:00:00 +0000 UTC
```

4. List the JSON configuration of the LVM plugin:

```bash
dcos storage plugin-configuration list --name lvm --json
```
```
{
    "plugin-configurations": [
        {
            "name": "lvm",
            "description": "Updated plugin configuration for lvm",
            "config-version": 2,
            "spec": {
                "csi-template": {
                    "services": [
                        "CONTROLLER_SERVICE",
                        "NODE_SERVICE"
                    ],
                    "command": {
                        "value": "{{.Cmdline | json }} -statsd-udp-host-env-var=STATSD_UDP_HOST -statsd-udp-port-env-var=STATSD_UDP_PORT",
                        "shell": true,
                        "environment": {
                            "CONTAINER_LOGGER_DESTINATION_TYPE": "journald+logrotate",
                            "CONTAINER_LOGGER_EXTRA_LABELS": "{\"CSI_PLUGIN\":\"csilvm\"}",
                            "DEBUG": "1",
                            "LD_LIBRARY_PATH": "/opt/mesosphere/lib",
                            "PATH": "/opt/mesosphere/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
                        },
                        "uris": [
                            {
                                "value": "file:///opt/mesosphere/active/dcos-csilvm/bin/csilvm",
                                "cache": true,
                                "executable": true
                            }
                        ]
                    },
                    "resources": [
                        {
                            "name": "cpus",
                            "value": 0.1
                        },
                        {
                            "name": "mem",
                            "value": 128
                        },
                        {
                            "name": "disk",
                            "value": 10
                        }
                    ]
                }
            },
            "created-at": "2019-01-13T13:00:00Z"
        }
    ]
}
```

### Options

Name | Description
--- | ---
`--all-versions` | Also show previous versions.
`--json` | Display the list of plugin configurations in json format.
`-n`,`--name` stringArray | Only show the named plugin configuration. May be specified multiple times.

### Options inherited from parent commands

Name | Description
--- | ---
`-h`,`--help` | Help for this command.
`--timeout` duration | Override the default operation timeout. (default 55s)
`-v`,`--verbose` | Verbose mode.

