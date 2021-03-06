---
layout: layout.pug
navigationTitle:  Release Notes for 1.10.8
title: Release Notes for 1.10.8
menuWeight: 10
excerpt:
---

DC/OS 1.10.8 was released on July 19, 2018.

[button color="purple" href="https://downloads.dcos.io/dcos/stable/1.10.8/dcos_generate_config.sh"]Download DC/OS Open Source[/button]
[button color="light" href="https://support.mesosphere.com/hc/en-us/articles/213198586"]Download DC/OS Enterprise[/button]

DC/OS 1.10.8 includes the following:
- Apache Mesos 1.4.2-5f6d4cd [change log](https://github.com/apache/mesos/blob/5f6d4cd/CHANGELOG).
- Marathon 1.5.11 [change log](https://github.com/mesosphere/marathon/releases/tag/v1.5.11).
- Metronome 0.4.2 [change log](https://github.com/dcos/metronome/releases/tag/v0.4.2).


# Issues Fixed in DC/OS 1.10.8

- COPS-1840/DCOS_OSS-3793 - Change Admin Router(nginx) log to access logs with the daemon facility.
- COPS-3180/DCOS-24373 - Fix odd exit behavior for tasks that use a volume mount (via rexray). [enterprise type="inline" size="small" /]
- COPS-3445/MESOS-8830 - Prevent Mesos agents from garbage-collecting persistent volumes.
- DCOS-18597/DCOS_OSS-3556 - Improve root Marathon support for post-installation configuration of flags and JVM settings. [enterprise type="inline" size="small" /]
- DCOS-37451 - Filter task labels used for book-keeping from appearing in metrics.
- DCOS-37452 - Increase the Mesos agent response timeout for dcos-metrics.
- DCOS-38083 - Improve the behaviour of `statsd` timers on dcos-metrics.
- DCOS_OSS-3304 - Add task labels as tags on container metrics.
- DCOS_OSS-3602 - Fix instability issue: L4LB is unstable during deployment of new VIPS.

# Notable Changes in DC/OS 1.10.8

- DCOS_OSS-3597 - Update REX-Ray version to [0.11.2](https://github.com/rexray/rexray/releases/tag/v0.11.2)

# About DC/OS 1.10

DC/OS 1.10.0 includes many new capabilities for operators and expands the collection of Data & Developer Services with a focus on:

- Core DC/OS service continuity - System resilience, IAM scalability & simplified upgrades.
- Robust security - Custom CA certificate & file-based secrets support. [enterprise type="inline" size="small" /]
- Enterprise-ready networking - New DC/OS Edge-LB for higher availability and security. [enterprise type="inline" size="small" /]
- Kubernetes is now available on DC/OS.
- Data services enhancements across the board.
  - Rolling configuration update and upgrade support via the CLI. [enterprise type="inline" size="small" /]
  - Ability to deploy Data Services into folders to enable multi team deployments. [enterprise type="inline" size="small" /]
  - Ability to deploy to CNI-Based virtual networks.

You can try out the new features and updated data services. Provide feedback through our support channel: <a href="https://support.mesosphere.com/">support.mesosphere.com</a>.

## New Features and Capabilities

### Networking
- Configurable Spartan upstreams for domains (dnames).
  You can now configure Spartan to delegate a particular domain (e.g. "\*.foo.company.com") to a particular upstream.

- Increased CNI network support.
  DC/OS now supports any type of CNI network. [View the documentation](/mesosphere/dcos/1.10/networking/virtual-networks/cni-plugins/).

- Edge-LB load balancer. [enterprise type="inline" size="small" /]

  Edge-LB load balances Mesos tasks. Not supported in strict security mode. [View the documentation](/mesosphere/dcos/services/edge-lb/latest/).

[enterprise type="block" size="large"]
### Security
[/ enterprise]

- Custom CA certificate support.
  Installation time [configuration options](/mesosphere/dcos/1.10/security/ent/tls-ssl/ca-custom/) have been added that allow you to configure DC/OS Enterprise to use a custom CA certificate and corresponding private key, which DC/OS then uses for issuing all component certificates. The custom CA certificate can be an intermediate CA certificate so that that all certificates used within the DC/OS cluster derive from your organization’s X.509 certification hierarchy.

- Enhanced secrets management with file-based secrets.
  You can now make a secret available to your service in the sandbox of the task. [View the documentation](/mesosphere/dcos/1.10/security/ent/secrets/use-secrets/).

- Vastly improved IAM scalability and performance characteristics.
  The new system removes hard limits on the number of users, groups, and permissions that can be stored, and shows stable read and write performance as the dataset grows.

- Docker `pullConfig` parameter.
  Use this parameter in your service definition to authenticate to a private Docker registry. [View the documentation](/mesosphere/dcos/1.10/deploying-services/private-docker-registry/#referencing-private-docker-registry-credentials-in-the-secrets-store-enterprise).

 - Enterprise CLI permissions management commands.
   It is now possible to manage permissions to protect resources using the [DC/OS Enterprise CLI](/mesosphere/dcos/1.10/security/ent/perms-management/).

### Kubernetes on DC/OS

- Kubernetes on DC/OS is beta with DC/OS 1.10.0. Install from the DC/OS Service Catalog or use the [quickstart](https://github.com/mesosphere/dcos-kubernetes-quickstart).

### Updated DC/OS Data Services

- Rolling Configuration Update and Upgrades support via the CLI. [enterprise type="inline" size="small" /]
- Ability to deploy Data Services into Folders to enable multi team deployments. [enterprise type="inline" size="small" /]
- Ability to deploy to CNI-Based Virtual Networks.

The following updated data services packages are compatible with DC/OS 1.10.0.

- Cassandra. [Documentation](/mesosphere/dcos/services/cassandra/latest/). [Release Notes](/mesosphere/dcos/services/cassandra/latest/release-notes/).

- Elastic. [Documentation](/mesosphere/dcos/services/elastic/latest/). [Release Notes](/mesosphere/dcos/services/elastic/latest/release-notes/).

- HDFS. [Documentation](/mesosphere/dcos/services/hdfs/latest/). [Release Notes](/mesosphere/dcos/services/hdfs/latest/release-notes/).

- Kafka. [Documentation](/mesosphere/dcos/services/kafka/latest/). [Release Notes](/mesosphere/dcos/services/kafka/latest/release-notes/).

- Apache Spark. [Documentation](/mesosphere/dcos/services/spark/latest/). [Release Notes](/mesosphere/dcos/services/spark/latest/release-notes/).

### Platform
- Node and cluster health checks.
  Write your own custom health checks or use the predefined checks to access and use information about your cluster, including available ports, Mesos agent status, and IP detect script validation. [View the documentation](/mesosphere/dcos/1.10/installing/production/deploying-dcos/node-cluster-health-check/).
- Enhanced upgrades with [backup and restore](/mesosphere/dcos/1.10/administering-clusters/backup-and-restore/), and pre/post flight checks. [enterprise type="inline" size="small" /]
- Universal Container Runtime (UCR).
  Adds port mapping support for containers running on the CNI network. Port mapping support allows UCR to have a default bridge network, similar to Docker's default bridge network. This gives UCR feature parity with Docker Engine enabling use of Mesos Runtime as the default container runtime.
- Scale and performance limits.

### CLI

- DC/OS 1.10.0 requires DC/OS CLI 0.5.x.
- DC/OS CLI 0.5.x adds [multi-cluster support](/mesosphere/dcos/1.10/cli/multi-cluster-cli/) with [`dcos cluster`](/mesosphere/dcos/1.10/cli/command-reference/dcos-cluster/) commands.


 Multi-cluster support has a number of consequences:

   - DC/OS CLI 0.4.x and 0.5.x use a different structure for the location of configuration files. DC/OS CLI 0.4.x has a single configuration file, which by default is stored in `~/.dcos/dcos.toml`. DC/OS CLI 0.5.x has a configuration file for each connected cluster, which by default are stored in `~/.dcos/clusters/<cluster_id>/dcos.toml`.
   - DC/OS CLI 0.5.x introduces the `dcos cluster setup` command to configure a connection to a cluster and log into the cluster.
   - **Note:**
     -  Updating to the DC/OS CLI 0.5.x and running any CLI command triggers conversion from the old to the new configuration structure.
     - _After_ you call `dcos cluster setup`, (or after conversion has occurred), if you attempt to update the cluster configuration using a `dcos config set` command, the command prints a warning message saying the command is deprecated and cluster configuration state may now be corrupted.
  - If you have the `DCOS_CONFIG` environment variable configured:
    - After conversion to the new configuration structure, `DCOS_CONFIG` is no longer honored.
    - _Before_ you call `dcos cluster setup`, you can change the configuration pointed to by `DCOS_CONFIG` using `dcos config set`. This command prints a warning message saying the command is deprecated and recommends using `dcos cluster setup`.
  - CLI modules are cluster-specific and stored in `~/.dcos/clusters/<cluster_id>/subcommands`. Therefore you must install a CLI module for each cluster. For example, if you connect to cluster 1, and install the Spark module, then connect to cluster 2 which is also running Spark, Spark CLI commands are not available until you install the module for that cluster.

### GUI
The GUI sidebar tabs have been updated to offer a more intuitive experience.

- The "Deployments" subpage under the "Services" tab has been moved to a toggle-able modal in the "Services" page.
- The "Security" tab has been removed. The "Secrets" tab that used to be under "Security" is now a top-level tab. [enterprise type="inline" size="small" /]
- The "Universe" tab has been renamed to "Catalog" and the "Installed" subpage has been removed.
- The "System Overview" tab has been renamed to "Overview".


## Breaking Changes

- Marathon Networking API Changes in 1.5.

  The networking section of the Marathon API has changed significantly in version 1.5. Marathon can still accept requests using the 1.4 version of the API, but it will always reply with the 1.5 version of the app definition. This will break tools that consume networking-related fields of the service definition. [View the documentation](https://github.com/mesosphere/marathon/blob/master/docs/docs/networking.md).

- TLS 1.0 is no longer enabled by default in Admin Router. [enterprise type="inline" size="small" /]

  TLS 1.0 no longer meets common minimum security requirements. To use TLS 1.0, set `adminrouter_tls_1_0_enabled` to `true` in your `config.yaml` at install time. The default is `false`.

- Moved file location for the DC/OS CA bundle in the sandbox of Mesos tasks from `$MESOS_SANDBOX/.ssl/ca.crt` to `$MESOS_SANDBOX/.ssl/ca-bundle.crt` and declared the new file path to be stable.

- Marathon-LB 1.11.0 or greater is required for DC/OS 1.10.0.

  Before upgrading to DC/OS 1.10.0, uninstall your existing Marathon-LB package and reinstall the updated version.

- REX-Ray configuration change.

  DC/OS 1.10.0 upgrades REX-Ray from v0.3.3 to v0.9.0 and the REX-Ray configuration format has changed. If you have specified custom REX-Ray configuration in the [`rexray_config`](/mesosphere/dcos/1.10/installing/production/advanced-configuration/configuration-reference/#rexray-config) parameter of your `config.yaml` file, either update the configuration to the new format or remove `rexray_config` and set the parameter to `rexray_config_preset: aws`, which configures the `rexray_config` parameter to the default REX-Ray configuration bundled with DC/OS. This option has the benefit of automatically upgrading your cluster's REX-Ray configuration when you upgrade to a newer version of DC/OS.
  **Note:** The `rexray_config_preset: aws` option is only relevant to DC/OS clusters running on AWS.

- New flow to change the `dcos_url` and log in.

  The new command to set up your cluster URL is `dcos cluster setup <dcos_url>`. For details, see [CLI](#cli).

- Hard CFS CPU limits enabled by default.

  DC/OS 1.10 enforces hard CPU limits with CFS isolation for both the Docker and Universal Container Runtimes. This will give more predictable performance across all tasks but might lead to a slowdown for tasks (and thereby also deployments) who have previously have consumed more CPU cycles than allocated. See [MESOS-6134](https://issues.apache.org/jira/browse/MESOS-6134) for more details.

## Known Issues
- Upgrade: During upgrade to DC/OS 1.10, there is a brief moment when the DNS resolution does not work. If a health check runs at that moment, it will fail and services will be reported as unhealthy.
- CORE-1125 - Docker image pull config is re-used.
- DCOS-16547 - Task state does not update after the agent running it was removed from the cluster.
- INFINITY-1809 - [Data Svc] DC/OS Service Update / Config Update / Maintenance. [enterprise type="inline" size="small" /]
- MARATHON-7736 - Marathon Client Java library does NOT work with Marathon 1.5.
