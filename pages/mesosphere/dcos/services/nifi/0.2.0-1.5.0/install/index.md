---
layout: layout.pug
navigationTitle:  Installing and Customizing
title: Installing and Customizing
menuWeight: 20
excerpt: Installing DC/OS NiFi from the UI or the CLI
featureMaturity:
enterprise: false
---

 DCOS NiFi is available in the Universe and can be installed by using either the UI or the DC/OS CLI.

The default DC/OS NiFi Service installation provides reasonable defaults for trying out the service, but that may not be sufficient for production use. You may require different configurations depending on the context of the deployment.

## Prerequisites

- If you are using DC/OS Enterprise, you may [need to provision a service account](/mesosphere/dcos/1.10/security/ent/service-auth/custom-service-auth/) before installing DC/OS NiFi Service. Only someone with `superuser` permission can create the service account.
- `strict` [security mode](/mesosphere/dcos/1.10/security/ent/service-auth/custom-service-auth/) requires a service account.
    A complete guide to Configuring DC/OS Access for NiFi can be found [here](/mesosphere/dcos/services/nifi/configure-dcos-access/).
- In `permissive` security mode a service account is optional.
- `disabled` security mode does not require a service account.
- Your cluster must have at least 3 private nodes.

# Installing from the DC/OS CLI

To start a basic test cluster of NiFi, run the following command on the DC/OS CLI. DC/OS Enterprise users must follow additional instructions.

   ```shell
   dcos package install nifi
   ```

This command creates a new instance with the default name `nifi`. Two instances cannot share the same name, so installing additional instances beyond the default instance requires customizing the name at install time for each additional instance. However, the application can be installed using the same name in case of foldered installation, weherein we can install the same application in different folders.

All `dcos nifi` CLI commands have a `--name` argument allowing you to specify which instance to query. If you do not specify a service name, the CLI assumes a default value matching the package name, such as `nifi`. The default value for `--name` can be customized via the DC/OS CLI configuration:

   ```shell
   dcos nifi --name=nifi <cmd>
   ```

You can specify a custom configuration in an `options.json` file and pass it to `dcos package install` using the `--options` parameter.

   ```shell
   dcos package install nifi --options=options.json
   ```

For more information on building the `options.json` file, see [DC/OS documentation](/mesosphere/dcos/1.12/deploying-services/config-universe-service/) for service configuration access.

## Installing from the DC/OS Web Interface

<p class="message--note"><strong>NOTE: </strong>Alternatively, you can install NiFi from the DC/OS UI by clicking on <strong>Deploy</strong> after selecting the app from the Catalog.</p>

If you install Apache NiFi from the DC/OS UI, the `dcos nifi` CLI commands are not automatically installed to your workstation. You can install them manually using the DC/OS CLI:


   ```shell
   dcos package install nifi --cli
   ```

## Installing multiple instances

By default, the Apache NiFi service is installed with a service name of `nifi`. You may specify a different name using a custom service configuration as follows:

   ```shell
   {
       "service": {
           "name": "nifi-other"
       }
   }
   ```

When the above JSON configuration is passed to the `package install nifi` command via the `--options` argument, the new service will use the name specified in that JSON configuration:

   ```shell
   dcos package install nifi --options=nifi-other.json
   ```

Multiple instances of Apache NiFi may be installed on your DC/OS cluster by customizing the name of each instance. For example, you might have one instance of Apache NiFi named `nifi-staging` and another named `nifi-prod`, each with its own custom  configuration.

After specifying a custom name for your instance, it can be reached using the `dcos nifi` CLI commands or directly over HTTP as described below.

<p class="message--important"><strong>IMPORTANT: </strong>The service name cannot be changed after initial install. Changing the service name would require installing a new instance of the service against the new name, then copying over any data as necessary to the new instance.</p>

## Installing into folders

In DC/OS 1.10 and later, services may be installed into folders by specifying a slash-delimited service name. For example:

   ```shell
   {
       "service": {
           "name": "/foldered/path/to/nifi"
       }
   }
   ```
The above example will install the service under a path of `foldered => path => to => nifi`. It can then be reached using `dcos nifi` CLI commands or directly over HTTP as described below.

<p class="message--note"><strong>NOTE: </strong><br>1) The service folder location cannot be changed after initial install. Changing the service location would require installing a new instance of the service against the new location, then copying over any data as necessary to the new instance.<br>2) `cn dn node identity` parameter specify `initial node identity` for TLS which will be used inside authorizers.xml file for CN value. </p>

## Addressing named instances

After you have installed the service under a custom name or under a folder, it may be accessed from all `dcos nifi` CLI commands using the `--name` argument. By default, the `--name` value defaults to the name of the package, or `nifi`.

For example, if you had an instance named `nifi-dev`, the following command would invoke a `pod list` command against it:

   ```shell
   dcos nifi --name=nifi-dev pod list
   ```
The same query would be over HTTP as follows:

   ```shell
   curl -H "Authorization:token=$auth_token" <dcos_url>/service/nifi-dev/v1/pod
   ```
Likewise, if you had an instance in a folder like `/foldered/path/to/nifi`, the following command would invoke a `pod list` command against it:

   ```shell
   dcos nifi --name=/foldered/path/to/nifi pod list
   ```

Similarly, it could be queried directly over HTTP as follows:

   ```shell
   curl -H "Authorization:token=$auth_token" <dcos_url>/service/foldered/path/to/nifi-dev/v1/pod
   ```
<p class="message--note"><strong>NOTE: </strong> You may add a `-v` (verbose) argument to any `dcos nifi` command to see the underlying HTTP queries that are being made. This can be a useful tool to see where the CLI is getting its information. In practice, `dcos nifi` commands are a thin wrapper around an HTTP interface provided by the DC/OS Apache NiFi Service itself.</p>

## Virtual Networks

DC/OS Apache NiFi supports deployment on virtual networks on DC/OS, allowing each container (task) to have its own IP address and not use port resources on the agent machines. This can be specified by passing the following configuration during installation:

   ```shell
   {
       "service": {
           "virtual_network_enabled": true
       }
   }
   ```
<p class="message--note"><strong>NOTE: </strong>Once the service is deployed on a virtual network, it cannot be updated to use the host network.</p>


## Minimal Installation

For development purposes, you may wish to install Apache NiFi on a local DC/OS cluster. For this, you can use `dcos-docker` or `dcos-vagrant`.
To start a minimal cluster with a single node, create a JSON options file named `sample-nifi-minimal.json`:

   ```shell
   {
       "node": {
       "count": 1,
       "mem": 512,
       "cpu": 0.5
       }
   }
   ```
The following command creates a cluster using `sample-nifi-minimal.json`:


   ```shell
   dcos package install nifi --options=sample-nifi-minimal.json
   ```
## Example custom installation

Customize the defaults by creating a JSON file. Then, pass it to `dcos package install` using the `--options` parameter.

Sample JSON options file named `sample-nifi-custom.json`:

   ```json
   {
   "node": {
       "count": 1,
       "cpus": 1
       },
   "service": {
       "name": "test/integration/nifi",
       "security": {
           "kerberos": {
               "enabled": true,
               "cn_dn_node_identity": "testintegrationnifi"
           },
           "tls_ssl": {
               "enable": true
           }
       },
       "service_account": "dcosnifi",
       "service_account_secret": "dcosnifisecret",
       "virtual_network_enabled": true
       }
   }
   ```
The command below creates a cluster using sample-nifi.json:
   ```shell
   dcos package install nifi --options=sample-nifi-custom.json
   ```
Store your custom configuration in source control.

Alternatively, you can perform a custom installation from the DC/OS UI. Choose ADVANCED INSTALLATION at install time.

## Integration with DC/OS access controls

In DC/OS Enterprise 1.10 and later, you can integrate your SDK-based service with DC/OS ACLs to grant users and groups access only to certain services. You do this by installing your service into a folder, and then restricting access to some number of folders. Folders also allow you to namespace services; for instance, `staging/nifi` and `production/nifi`.

Steps:

  1. In the DC/OS GUI, create a group, then add a user to the group. Or, just create a user. Click **Organization > Groups > + or Organization > Users > +**. If you create a group, you must also create a user and add them to the group.

  2. Give the user permissions for the folder where you will install your service. In this example, we are creating a user called developer, who will have access to the `/testing` folder.

  3. Select the group or user you created. Select ADD PERMISSION and then toggle to INSERT PERMISSION STRING. Add each of the following permissions to your user or group, and then click ADD PERMISSIONS.

   ```shell
   dcos:adminrouter:service:marathon full
   dcos:service:marathon:marathon:services:/testing full
   dcos:adminrouter:ops:mesos full
   dcos:adminrouter:ops:slave full
   ```
  4. Install your service into a folder called `test`. Go to the Catalog, then search for `nifi`.

  5. Click CONFIGURE and change the service name to `/testing/nifi`, then deploy.
The slashes in your service name are interpreted as folders. You are deploying `nifi` in the `/testing` folder. Any user with access to the `/testing` folder will have access to the service.

<p class="message--important"><strong>IMPORTANT: </strong>Services cannot be renamed. Because the location of the service is specified in the name, you cannot move services between folders. Also, DC/OS versions 1.9 and earlier do not accept slashes in service names. You may be able to create the service, but you will encounter unexpected problems.</p>

## Interacting with your foldered service

1. Interact with your foldered service via the DC/OS CLI with this flag: `--name=/path/to/myservice`.
2. To interact with your foldered service over the web directly, use [http://<dcos-url>/service/path/to/myservice](http://<dcos-url>/service/path/to/myservice). For example, [http://<dcos-url>/service/testing/nifi/v1/endpoints](http://<dcos-url>/service/testing/nifi/v1/endpoints).

## Placement Constraints

Placement constraints allow you to customize where a service is deployed in the DC/OS cluster. Depending on the service, some or all components may be configurable using Marathon operators (reference). For example, [["hostname", "UNIQUE"]] ensures that at most one pod instance is deployed per agent.

A common task is to specify a list of whitelisted systems to deploy to. To achieve this, use the following syntax for the placement constraint:
   ```shell
   [["hostname", "LIKE", "10.0.0.159|10.0.1.202|10.0.3.3"]]
   ```
You must include spare capacity in this list, so that if one of the whitelisted systems goes down, there is still enough room to repair your service (via `pod replace`) without requiring that system.

**Example: **

In order to define placement constraints as part of an install or update of a service, they should be provided as a JSON encoded string. For example, you can define a placement constraint in an options file as follows:

   ```shell
   cat options.json
   {
       "hello": {
       "placement": "[[\"hostname\", \"UNIQUE\"]]"
       }
   }
   ```
This file can be referenced to install a `nifi` service.

   ```shell
   dcos package install hello-world --options=options.json
   ```
Likewise, this file can be referenced to update a `nifi` service.

   ```shell
   dcos nifi update start --options=options.json
   ```

## Secured Installation
Please refer to the Security guide for info about a secured installation of [NiFi](/mesosphere/dcos/services/nifi/0.3.0-1.7.1/security/)
