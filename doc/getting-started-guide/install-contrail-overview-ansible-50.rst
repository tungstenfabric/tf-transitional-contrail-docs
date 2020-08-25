.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

====================================================================================================================================
Overview of contrail-ansible-deployer used in Contrail Command for Installing Tungsten Fabric with Microservices Architecture
====================================================================================================================================

Tungsten Fabric Release 5.0 introduces microservices architecture. This section provides an overview of using ``contrail-ansible-deployer`` used by The Contrail Command tool for installing Tungsten Fabric Networking with a microservices architecture. For an introduction to Tungsten Fabric microservices, refer to. For step by step procedure on how to install contrail using contrail command deployer, refer to Deploying Tungsten Fabric Cluster using Contrail-Command and instances.yml

-  `What is the contrail-ansible-deployer?`_ 


-  `Preparing to Install with Tungsten Fabric`_ 


-  `Supported Providers`_ 


-  `Configure a Yaml File for Your Environment`_ 


-  `Installing a Tungsten Fabric System`_ 


What is the contrail-ansible-deployer?
--------------------------------------

The ``contrail-ansible-deployer`` is a set of Ansible playbooks designed to deploy Tungsten Fabric 5.x with microservices architecture.

The ``contrail-ansible-deployer`` contains three plays:

-  `playbooks/provision_instances.yml`_ 


-  `playbooks/configure_instances.yml`_ 


-  `playbooks/install_contrail.yml`_ 


playbooks/provision_instances.yml
---------------------------------

This play provisions the operating system instances for hosting the containers, currently for these infrastructure providers:

- kvm


- gce


- aws


playbooks/configure_instances.yml
---------------------------------

This play configures the provisioned instances. The playbook installs software and configures the operating system to meet prerequisite standards. This is applicable to all providers.

playbooks/install_contrail.yml
------------------------------

This play pulls, configures, and starts the Tungsten Fabric containers.

Preparing to Install with Tungsten Fabric
-----------------------------------------

This section helps you prepare your system before installing Tungsten Fabric 5.0. *x* using ``contrail-command-deployer`` .

Prerequisites
-------------

Make sure your system is operational with the following before installation with ``contrail-command-deployer`` .

- CentOS 7.4, kernel >= 3.10.0-693.17.1


- Ansible 2.4.2.0


- Name resolution is operational for long and short host names of the cluster nodes, through either DNS or the host file.


- Docker engine (tested version is 17.03.1-ce)


- The docker-compose installed (tested version is 1.17.0)


- The docker-compose Python library (tested version is 1.9.0)


- If using Kubernetes (k8s), the tested version is 1.9.2.0


- For high availability (HA), the time must be in sync between the cluster nodes.




Supported Providers
-------------------

The playbooks support installing Tungsten Fabric on the following providers:

- bms—bare metal server


- kvm—kernel-based virtual machine (KVM)-hosted virtual machines


- gce—Google compute engine (GCE)-hosted virtual machines


- aws—Amazon Web Services (AWS)-hosted virtual machines




Configure a Yaml File for Your Environment
------------------------------------------

The configuration for all three plays is contained in a single file:

``config/instances.yaml`` 

The configuration has multiple main sections, including:

-  `Provider Configuration`_ 


-  `Global Services Configuration`_ 


-  `Tungsten Fabric Services Configuration`_ 


-  `Kolla Services Configuration`_ 


-  `Instances Configuration`_ 


The main sections of the ``config/instances.yaml`` file are described in this section. Using the sections that are appropriate for your system, configure each with parameters specific to your environment.



Provider Configuration
-----------------------

The section ``provider_config`` configures provider-specific settings.

KVM Provider Example
--------------------

Use this example if you are in a kernel-based virtual machine-hosted environment.
::

  provider_config:                                   # the provider section contains all provider relevant configuration
  kvm:                                                    # Mandatory.
  image: CentOS-7-x86_64-GenericCloud-1710.qcow2.xz     # Mandatory for provision play. Image to be deployed.
  image_url: https://cloud.centos.org/centos/7/images/  # Mandatory for provision play. Path/url to image.
  ssh_pwd: contrail123                                  # Mandatory for provision/configuration/install play. Ssh password set/used.
  ssh_user: centos                                      # Mandatory for provision/configuration/install play. Ssh user set/used.
  ssh_public_key: /home/centos/.ssh/id_rsa.pub          # Optional for provision/configuration/install play.
  ssh_private_key: /home/centos/.ssh/id_rsa             # Optional for provision/configuration/install play.
  vcpu: 12                                              # Mandatory for provision play.
  vram: 64000                                           # Mandatory for provision play.
  vdisk: 100G                                           # Mandatory for provision play.
  subnet_prefix: ip-address                           # Mandatory for provision play.
  subnet_netmask: subnet-mask                         # Mandatory for provision play.
  gateway: gateway-ip-address                                  # Mandatory for provision play.
  nameserver: dns-ip-address                               # Mandatory for provision play.
  ntpserver: ntp-server-ip-address                                # Mandatory for provision/configuration play.
  domainsuffix: local                                   # Mandatory for provision play.



BMS Provider Example
--------------------

Use this example if you are in a bare metal server environment.
::

  provider_config:
  bms:                                            # Mandatory.
  ssh_pwd: contrail123                          # Optional. Not needed if ssh keys are used.
  ssh_user: centos                              # Mandatory.
  ssh_public_key: /home/centos/.ssh/id_rsa.pub  # Optional. Not needed if ssh password is used.
  ssh_private_key: /home/centos/.ssh/id_rsa     # Optional. Not needed if ssh password is used.
  ntpserver: ntp-server-ip-address                        # Optional. Needed if ntp server should be configured.
  domainsuffix: local                           # Optional. Needed if configuration play should configure /etc/hosts



AWS Provider Example
--------------------

Use this example if you are in an Amazon Web Services environment.
::

  provider_config:
  aws:                                            # Mandatory.
  ec2_access_key: THIS_IS_YOUR_ACCESS_KEY       # Mandatory.
  ec2_secret_key: THIS_IS_YOUR_SECRET_KEY       # Mandatory.
  ssh_public_key: /home/centos/.ssh/id_rsa.pub  # Optional.
  ssh_private_key: /home/centos/.ssh/id_rsa     # Optional.
  ssh_user: centos                              # Mandatory.
  instance_type: t2.xlarge                      # Mandatory.
  image: ami-337be65c                           # Mandatory.
  region: eu-central-1                          # Mandatory.
  security_group: SECURITY_GROUP_ID             # Mandatory.
  vpc_subnet_id: VPC_SUBNET_ID                  # Mandatory.
  assign_public_ip: yes                         # Mandatory.
  volume_size: 50                               # Mandatory.
  key_pair: KEYPAIR_NAME                        # Mandatory.



GCE Provider Example
--------------------

Use this example if you are in a Google Cloud environment.
::

  provider_config:
  gce:                           # Mandatory.
  service_account_email:       # Mandatory. GCE service account email address.
  credentials_file:            # Mandatory. Path to GCE account json file.
  project_id:                  # Mandatory. GCE project name.
  ssh_user:                    # Mandatory. Ssh user for GCE instances.
  ssh_pwd:                     # Optional.  Ssh password used by ssh user, not needed when public is used
  ssh_private_key:             # Optional.  Path to private SSH key, used by by ssh user, not needed when ssh-agent loaded private key
  machine_type: n1-standard-4  # Mandatory. Default is too small
  image: centos-7              # Mandatory. For provisioning and configuration only centos-7 is currently supported.
  network: microservice-vn     # Optional.  Defaults to default
  subnetwork: microservice-sn  # Optional.  Defaults to default
  zone: us-west1-aA            # Optional.  Defaults to  ?
  disk_size: 50                # Mandatory. Default is too small



Global Services Configuration
-----------------------------

This section sets global service parameters. All parameters are optional.
::

  global_configuration:
  CONTAINER_REGISTRY: opencontrailnightly
  REGISTRY_PRIVATE_INSECURE: True
  CONTAINER_REGISTRY_USERNAME: YourRegistryUser
  CONTAINER_REGISTRY_PASSWORD: YourRegistryPassword



Tungsten Fabric Services Configuration
--------------------------------------

This section sets global Tungsten Fabric service parameters. All parameters are optional.
::

  contrail_configuration:     # Tungsten Fabric service configuration section
  CONTRAIL_VERSION: latest
  UPGRADE_KERNEL: true


For a complete list of parameters available for contrail_configuration.md, see Tungsten Fabric Configuration Parameters for Ansible Deployer.



Kolla Services Configuration
----------------------------

If OpenStack Kolla is deployed, this section defines the parameters for Kolla.
::

  kolla_config:




Instances Configuration
-----------------------

Instances are the operating systems on which the containers will be launched. The instance configuration has a few provider-specific knobs. The instance configuration specifies which roles are installed on which instance. Additionally, instance-wide and role-specific Tungsten Fabric and Kolla configurations can be specified, overwriting the parameters from the global Tungsten Fabric and Kolla configuration settings.



GCE Default All-in-One Instance
-------------------------------

The following example is a very simple all-in-one GCE instance. It will install all Tungsten Fabric roles and the Kubernetes master and node, using the default configuration.
::

  instances:
  gce1:                          # Mandatory. Instance name
  provider: gce                # Mandatory. Instance runs on GCE



AWS Default All-in-One Instance
-------------------------------

The following example uses three AWS EC2 instances to deploy, and an all-in-one high availability setup with all roles and default parameters.
::

  instances:
  aws1:
    provider: aws
  aws2:
    provider: aws
  aws3:
    provider: aws



KVM Tungsten Fabric Plane Instance
---------------------------

The following example is a KVM-based instance only, installing Tungsten Fabric control plane containers.
::

  instances:
  kvm1:
  provider: kvm
  roles:
    config_database:
    config:
    control:
    analytics_database:
    analytics:
    webui:
    kubemanager:
    k8s_master:



More Examples
-------------

Refer to the following for more configuration examples for instances.

-  `GCE Kubernetes (k8s) HA with separate control and data plane instances`_  


-  `AWS Kolla HA with separate control and data plane instances`_  

Installing a Tungsten Fabric System
-----------------------------------

To perform a full installation of a Tungsten Fabric system, refer to the installation instructions in: Deploying Tungsten Fabric Cluster using Contrail-Command and instances.yml

**Related Documentation**

- Deploying Tungsten Fabric Cluster using Contrail-Command and instances.yml


.. _Introduction to Tungsten Fabric Microservices Architecture: 

.. _Deploying Tungsten Fabric Cluster using Contrail-Command and instances.yml: 

.. _Tungsten Fabric Configuration Parameters for Ansible Deployer: 

.. _GCE Kubernetes (k8s) HA with separate control and data plane instances: https://github.com/Juniper/contrail-ansible-deployer/blob/master/examples/gce1.md

.. _AWS Kolla HA with separate control and data plane instances: https://github.com/Juniper/contrail-ansible-deployer/blob/master/examples/aws1.md
