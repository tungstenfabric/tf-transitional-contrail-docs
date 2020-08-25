.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===========================================================
Installing Tungsten Fabric with OpenStack and Kolla Ansible
===========================================================

This topic provides the steps needed to install Tungsten Fabric Release 5.0.x. with OpenStack, using Kolla Ansible playbook ``contrail-kolla-ansible`` . Kolla is an OpenStack project that provides Docker containers and Ansible playbooks to provide production-ready containers and deployment tools for operating OpenStack clouds.

The ``contrail-kolla-ansible`` playbook works in conjunction with ``contrail-ansible-deployer`` to install OpenStack and Release 5.0. *x* . containers.

To deploy a Tungsten Fabric Cluster using Contrail Command, see Deploying Tungsten Fabric Cluster using Contrail-Command and instances.yml.

Deployment of Kolla containers using ``contrail-kolla-ansible`` and Tungsten Fabric containers using ``contrail-ansible-deployer`` is presented in this topic:

-  `Set Up the Base Host`_ 


-  `Run OpenStack Commands`_ 


-  `Multiple Interface Configuration Sample for Multinode OpenStack HA and Tungsten Fabric`_ 


-  `Single Interface Configuration Sample for Multinode OpenStack HA and Tungsten Fabric`_ 


-  `Frequently Asked Questions`_ 




Set Up the Base Host
--------------------

This procedure assumes you are installing with CentOS 7.5 kernel 3.10.0-862.11.6.el7.x86_64. The vRouter has a `dependency`_  with the host kernel. Install this kernel version on the target nodes before provisioning.

To set up the base host:


#. Install Ansible.

   ``yum -y install epel-release`` 

   ``yum -y install git ansible-2.4.2.0`` 



#. Configure Tungsten Fabric and Kolla parameters in the file ``instances.yaml`` , using the following guidelines:

   - The provider configuration ( ``provider_config`` ) section refers to the cloud provider where the Tungsten Fabric cluster will be hosted, and contains all parameters relevant to the provider. For bare metal servers, the provider is ``bms`` .


   - The ``kolla_globals`` section refers to OpenStack services. For more information about all possible ``kolla_globals`` , see `https://github.com/Juniper/contrail-kolla-ansible/.../globals.yml`_  .


   - Additional Kolla configurations ( ``contrail-kolla-ansible`` ) are possible as ``contrail_additions`` . For more information about all possible ``contrail_additions`` to Kolla, see `https://github.com/Juniper/contrail-kolla-ansible/.../all.yml`_  .


   - The ``contrail_configuration`` section contains parameters for Tungsten Fabric services.

     -  ``CONTAINER_REGISTRY`` specifies the registry from which to pull Tungsten Fabric containers. It can be set to your local Docker registry if you are building your own containers. If a registry is not specified, it will try to pull the containers from the Docker hub.

         If a custom registry is specified, also specify the same registry under ``kolla_globals`` as ``contrail_docker_registry`` .


     -  ``CONTRAIL_VERSION`` , if not specified, will default to the "latest" tag. It is possible to specify a tag from nightly builds.


     - For more information about all possible parameters for ``contrail_configuration`` , see `https://github.com/Juniper/contrail-container-builder/.../common.sh`_  .


     - If “roles” is not specified, the following roles are assumed.

     ::

       config_database:
       config:
       control:
       analytics_database:
       analytics:
       webui:
       vrouter:
       openstack:
       openstack_compute:


     - If there are host-specific values per host, for example, if the names of the interfaces used for "network_interface" are different on the servers in your cluster, use the example configuration at `Configuration Sample for Multi Node OpenStack HA and Tungsten Fabric (multi interface)`_  .


     - Many of the parameters are automatically derived to sane defaults (how the first configuration works). You can explicitly specify variables to override the derived values if required. Review the code to see the derivation logic.


     - CONTROL_DATA_NET_LIST can be a comma separated list of CIDR subnets that can be designated for CONTROL/DATA plane traffic. The 'kolla' parameters 'network_interface' will be derived from this subnet as the interface that corresponds to an IP address in this subnet. CONTROL_DATA_NET_LIST can still be used in a single interface setup by specifying the management subnet as the value so that the interface names need not be specified.




Example: instances.yaml
~~~~~~~~~~~~~~~~~~~~~~~

This example is a bare minimum configuration for a single node, single interface, all-in-one cluster.
::

 provider_config:
 bms:
   ssh_pwd: <password>
   ssh_user: root
   ntpserver: <IP NTP server>    domainsuffix: local
 instances:
   bms1:
     provider: bms
     ip: <IP BMS>1
 contrail_configuration:
   RABBITMQ_NODE_PORT: 5673
   AUTH_MODE: keystone
   KEYSTONE_AUTH_URL_VERSION: /v3
 kolla_config:
   kolla_globals:
     enable_haproxy: no
   kolla_passwords:
     keystone_admin_password: <Keystone admin password>


Example: instances.yaml
~~~~~~~~~~~~~~~~~~~~~~~

This example is a more elaborate configuration for a single node, single interface, all-in-one cluster.
::

 Cprovider_config:
 bms:
    ssh_pwd: <password>
    ssh_user: root
    ntpserver: <IP NTP server>
    domainsuffix: local
 instances:
   bms1:
     provider: bms
     ip: <IP BMS>
     roles:
       config_database:
       config:
       control:
       analytics_database:
       analytics:
       webui:
       vrouter:
       openstack:
       openstack_compute:
 global_configuration:
   CONTAINER_REGISTRY: <Registry FQDN/IP>:<Registry Port>
   REGISTRY_PRIVATE_INSECURE: True
 contrail_configuration:
   CONTRAIL_VERSION: latest
   CLOUD_ORCHESTRATOR: openstack
   VROUTER_GATEWAY: <IP gateway>
   RABBITMQ_NODE_PORT: 5673
   PHYSICAL_INTERFACE: <interface name>
   AUTH_MODE: keystone
   CONTROL_DATA_NET_LIST: 198.168.10.0/24
   KEYSTONE_AUTH_URL_VERSION: /v3
 kolla_config:
   kolla_globals:
     kolla_internal_vip_address: <Internal VIP>
     contrail_api_interface_address: <Tungsten Fabric API Addr>
     enable_haproxy: no
   kolla_passwords:
     keystone_admin_password: <Keystone Admin Password>
  



3. Follow the steps documented Deploying Tungsten Fabric Cluster using Contrail-Command and instances.yml.


Run OpenStack Commands
----------------------

At this time, it is necessary to manually install the OpenStack client ( ``python-openstackclient)`` using pip. You cannot install using Yum repos because some dependent Python libraries conflict with the installation of the ``python-openstackclient`` . You also cannot install using pip repos because Ansible libraries can be overwritten.


#. Manually install the ``python-openstackclient`` .

   ``yum install -y gcc python-devel`` 

   ``pip install python-openstackclient`` 

   ``pip install python-ironicclient`` 



#. Test the setup with VM-to-VM ping.

::

 source /etc/kolla/admin-openrc.sh
 wget http://download.cirros-cloud.net/0.4.0/cirros-0.4.0-x86_64-disk.img
 openstack image create cirros2 --disk-format qcow2 --public --container-format bare --file cirros-0.4.0-x86_64-disk.img                                      
 openstack network create testvn
 openstack subnet create --subnet-range 198.168.100.0/24 --network testvn subnet1
 openstack flavor create --ram 512 --disk 1 --vcpus 1 m1.tiny
 NET_ID=`openstack network list | grep testvn | awk -F '|' '{print $2}' | tr -d ' '`
 openstack server create --flavor m1.tiny --image cirros2 --nic net-id=${NET_ID} test_vm1
 openstack server create --flavor m1.tiny --image cirros2 --nic net-id=${NET_ID} test_vm2




Multiple Interface Configuration Sample for Multinode OpenStack HA and Tungsten Fabric
--------------------------------------------------------------------------------------

This is a configuration sample for a multiple interface, multiple node deployment of high availability OpenStack and Release 5.0.x. Use this sample to configure parameters specific to your system.

For more information or for recent updates, refer to the github topic `Configuration Sample for Multi Node OpenStack HA and Tungsten Fabric (multi interface).`_  



Configuration Sample—Multiple Interface
---------------------------------------


.. note:: This example shows host-specific parameters, where interface names are different on each host and are specified under each role. The most specific setting takes precedence. As an example, if there was no ``network_interface`` setting under the role ``openstack`` for ``bms1`` , then it would take the name value ``eth2`` from the global variable. However, because there is a setting under the ``bms1 openstack`` section, that ``network_interface`` name will be ``eno1`` .


::

  provider_config:
  bms:
    ssh_pwd: <Pwd>
    ssh_user: root
    ntpserver: <NTP Server>
    domainsuffix: local
 instances:
   bms1:
     provider: bms
     ip: <BMS1 IP>
     roles:
       openstack:
   bms2:
     provider: bms
     ip: <BMS2 IP>
     roles:
       openstack:
   bms3:
     provider: bms
     ip: <BMS3 IP>
     roles:
       openstack:
   bms4:
     provider: bms
     ip: <BMS4 IP>
     roles:
       config_database:
       config:
       control:
       analytics_database:
       analytics:
       webui:
   bms5:
     provider: bms
     ip: <BMS5 IP>
     roles:
       config_database:
       config:
       control:
       analytics_database:
       analytics:
       webui:
   bms6:
     provider: bms
     ip: <BMS6 IP>
     roles:
       config_database:
       config:
       control:
       analytics_database:
       analytics:
       webui:
   bms7:
     provider: bms
     ip: <BMS7 IP>
     roles:
       vrouter:
         PHYSICAL_INTERFACE: <Interface name>
         VROUTER_GATEWAY: <Gateway IP>
       openstack_compute:
   bms8:
     provider: bms
     ip: <BMS8 IP>
     roles:
       vrouter:
         # Add following line for TSN Compute Node
         TSN_EVPN_MODE: True
       openstack_compute:
 contrail_configuration:
   CLOUD_ORCHESTRATOR: openstack
   CONTROL_DATA_NET_LIST: <Control Data Subnet CIDR>
   KEYSTONE_AUTH_URL_VERSION: /v3
   IPFABRIC_SERVICE_HOST: <Service Host IP>
   # Add following line for TSN Compute Node
   TSN_NODES: <TSN NODE IP List>
   # For EVPN VXLAN TSN
   ENCAP_PRIORITY: "VXLAN,MPLSoUDP,MPLSoGRE"
   PHYSICAL_INTERFACE: <Interface name>
 kolla_config:
   kolla_globals:
     kolla_internal_vip_address: <Internal VIP>
     kolla_external_vip_address: <External VIP>
     contrail_api_interface_address: <Tungsten Fabric API IP>
   kolla_passwords:
     keystone_admin_password: <Keystone Admin Password>




Single Interface Configuration Sample for Multinode OpenStack HA and Tungsten Fabric
------------------------------------------------------------------------------------

This is a configuration sample for a multiple interface, single node deployment of high availability OpenStack and Release 5.0.x. Use this sample to configure parameters specific to your system.

For more information or for recent updates, refer to the github topic `Configuration Sample for Multi Node OpenStack HA and Tungsten Fabric (single interface).`_  



Configuration Sample—Single Interface
-------------------------------------
::

 provider_config:
 bms:
    ssh_pwd: <password>
    ssh_user: root
    ntpserver: xx.xx.x.xx
    domainsuffix: local
 instances:
   centos1:
     provider: bms
     ip: ip-address
     roles:
       openstack:
   centos2:
     provider: bms
     ip: ip-address
     roles:
       openstack:
   centos3:
     provider: bms
     ip: ip-address
     roles:
       openstack:
   centos4:                                                       
     provider: bms
     ip: ip-address
     roles:
       config_database:
       config:
       control:
       analytics_database:
       analytics:
       webui:
   centos5:
     provider: bms
     ip: ip-address
     roles:
       config_database:
       config:
       control:
       analytics_database:
       analytics:
       webui:
   centos6:
     provider: bms
     ip: ip-address
     roles:
       config_database:
       config:
       control:
       analytics_database:
       analytics:
       webui:
   centos7:
     provider: bms
     ip: ip-address
     roles:
       vrouter:
       openstack_compute:
   centos8:
     provider: bms
     ip: ip-address
     roles:
       vrouter:
       openstack_compute:
 contrail_configuration:
   CONTRAIL_VERSION: master-centos7-ocata-bld-3
   CONTROLLER_NODES: ip-addresses separated by comma
   CLOUD_ORCHESTRATOR: openstack
   RABBITMQ_NODE_PORT: 5673
   VROUTER_GATEWAY: gateway-ip-address
   PHYSICAL_INTERFACE: eth1
   IPFABRIC_SERVICE_IP: ip-address
   KEYSTONE_AUTH_HOST: ip-address
   KEYSTONE_AUTH_URL_VERSION: /v3
 kolla_config:
   kolla_globals:
     kolla_internal_vip_address: ip-address
     contrail_api_interface_address: ip-address
     network_interface: "eth1"
     enable_haproxy: "yes"
   kolla_passwords:
     keystone_admin_password: <password>



Frequently Asked Questions
--------------------------

This section presents some common error situations and gives guidance on how to resolve the error condition.

Using Host-Specific Parameters
------------------------------

You might have a situation where you need to specify host-specific parameters, for example, the interface names are different for the different servers in the cluster. In this case, you could specify the individual names under each role, and the more specific setting takes precedence.

For example, if there is no "network_interface" setting under the role "openstack" for example “bms1”, then it will take its setting from the global variable.

An extended example is available at: `Configuration Sample for Multi Node OpenStack HA and Tungsten Fabric`_  .



Containers from Private Registry Not Accessible
-----------------------------------------------

#. You might have a situation in which containers that are pulled from a private registry named CONTAINER_REGISTRY are not accessible.

#. To resolve, check to ensure that REGISTRY_PRIVATE_INSECURE is set to **True** .

Error: Failed to insert vrouter kernel module
---------------------------------------------


#. You might have a situation in which the vrouter module is not getting installed on the compute nodes, with the vrouter container in an error state and errors are shown in the Docker logs.
   ::

    [srvr5] ~ # docker logs vrouter_vrouter-kernel-init_1
    /bin/cp: cannot create regular file '/host/bin/vif': No such file or directory
    INFO: Load kernel module for kver=3.10.0
    INFO: Modprobing vrouter /opt/contrail/vrouter-kernel-modules/3.10.0-862.11.6.el7.x86_64/vrouter.ko
                  total        used        free      shared  buff/cache   available
    Mem:            62G        999M         55G        9.1M        5.9G         60G
    Swap:            0B          0B          0B
                  total        used        free      shared  buff/cache   available
    Mem:            62G        741M         61G        9.1M        923M         61G
    Swap:            0B          0B          0B
    insmod: ERROR: could not insert module /opt/contrail/vrouter-kernel-modules/3.10.0-862.11.6.el7.x86_64/vrouter.ko: Unknown symbol in module
    ERROR: Failed to insert vrouter kernel module



#. In this release, the vrouter module requires the host kernel version to be 3.10.0-862.11.6.el7.x86_64. To get this kernel version, before running provision, install the kernel version on the target nodes.
   ::

    yum -y install kernel-3.10.0-862.11.6.el7.x86_64                                                                                                                                                    
    yum update
    reboot




Fatal Error When Vrouter Doesn’t Specify OpenStack
--------------------------------------------------


#. You might encounter a fatal error when vrouter needs to be provisioned without nova-compute.
   ::

    2018-03-21 00:47:16,884 p=16999 u=root |  TASK [iscsi : Ensuring config directories exist] ********************

    2018-03-21 00:47:16,959 p=16999 u=root |  fatal: [ip-address]: FAILED! => {"msg": "The conditional check 
    'inventory_hostname in groups['compute'] or inventory_hostname in groups['storage']' failed. The error was: 
    error while evaluating conditional (inventory_hostname in groups['compute'] or inventory_hostname in 
    groups['storage']): Unable to look up a name or access an attribute in template string ({% if 
    inventory_hostname in groups['compute'] or inventory_hostname in groups['storage'] %} True {% else %} False 
    {% endif %}).\nMake sure your variable name does not contain invalid characters like '-': argument of type 
    'StrictUndefined' is not iterable\n\nThe error appears to have been in '/root/contrail-kolla-
    ansible/ansible/roles/iscsi/tasks/config.yml': line 2, column 3, but may\nbe elsewhere in the file depending 
    on the exact syntax problem.\n\nThe offending line appears to be:\n\n---\n- name: Ensuring config 
    directories exist\n  ^ here\n"}

    2018-03-21 00:47:16,961 p=16999 u=root |        to retry, use: --limit @/root/contrail-ansible-
    deployer/playbooks/install_contrail.retry



#. There is a use case in which vrouter needs to be provisioned without being accompanied by nova-compute. Consequently, the "openstack_compute" is not automatically inferred when "vrouter" role is specified. To resolve this issue, the "openstack_compute" role needs to be explicitly stated along with "vrouter".

For more information about this use case, refer to the bug # `1756133`_  .

Need for HAProxy and Virtual IP on a Single OpenStack Cluster
-------------------------------------------------------------

By default, all OpenStack services listen on the IP interface provided by the ``kolla_internal_vip_address/network_interface`` variables under the ``kolla_globals`` section in ``config/instances.yaml`` . In most cases this corresponds to the ctrl-data network, which means that even Horizon will now run only on the ctrl-data network. The only way Kolla provides access to Horizon on the management network is by using HAProxy and keepalived. Enabling keepalived requires a virtual IP for VRRP, and it cannot be the interface IP. There is no way to enable HAProxy without enabling keepalived when using Kolla configuration parameters. For this reason,you need to provide two virtual IP addresses: one on management ( ``kolla_external_vip_address`` ) and one on ctrl-data-network ( ``kolla_internal_vip_address`` ). With this configuration, Horizon will be accessible on the management network by means of the ``kolla_external_vip_address`` .



Using the kolla_toolbox Container to Run OpenStack Commands
-----------------------------------------------------------

The directory ``/etc/kolla/kolla-toolbox`` on the base host on which OpenStack containers are running is mounted and accessible as ``/var/lib/kolla/config_files`` from inside the ``kolla_toolbox`` container. If you need other files when executing OpenStack commands, for example the command ``openstack image create`` needs an image file, you can copy the relevant files into the ``/etc/kolla/kolla-toolbox`` directory of the base host and use them inside the container.

The following example shows how to run OpenStack commands in this way:
::

 # ON BASE HOST OF OPENSTACK CONTROL NODE
 cd /etc/kolla/kolla-toolbox
 wget http://download.cirros-cloud.net/0.4.0/cirros-0.4.0-x86_64-disk.img

 docker exec -it kolla_toolbox bash
 # NOW YOU ARE INSIDE THE KOLLA_TOOLBOX CONTAINER
 (kolla-toolbox)[ansible@server1 /]$ source /var/lib/kolla/config_files/admin-openrc.sh
 (kolla-toolbox)[ansible@server1 /]$ cd /var/lib/kolla/config_files
 (kolla-toolbox)[ansible@server1 /var/lib/kolla/config_files]$ openstack image create cirros2 --disk-format qcow2 --public --container-format bare --file cirros-0.4.0-x86_64-disk.img
 +------------------+------------------------------------------------------+
 | Field            | Value                                                |
 +------------------+------------------------------------------------------+
 | checksum         | 443b7623e27ecf03dc9e01ee93f67afe                     |
 | container_format | bare                                                 |
 | created_at       | 2018-03-29T21:37:48Z                                 |
 | disk_format      | qcow2                                                |
 | file             | /v2/images/e672b536-0796-47b3-83a6-df48a5d074be/file |
 | id               | e672b536-0796-47b3-83a6-df48a5d074be                 |
 | min_disk         | 0                                                    |
 | min_ram          | 0                                                    |
 | name             | cirros2                                              |
 | owner            | 371bdb766278484bbabf868cf7325d4c                     |
 | protected        | False                                                |
 | schema           | /v2/schemas/image                                    |
 | size             | 12716032                                             |
 | status           | active                                               |
 | tags             |                                                      |
 | updated_at       | 2018-03-29T21:37:50Z                                 |
 | virtual_size     | None                                                 |
 | visibility       | public                                               |
 +------------------+------------------------------------------------------+
 (kolla-toolbox)[ansible@server1 /var/lib/kolla/config_files]$ openstack image list
 +--------------------------------------+---------+--------+
 | ID                                   | Name    | Status |
 +--------------------------------------+---------+--------+
 | e672b536-0796-47b3-83a6-df48a5d074be | cirros2 | active |
 | 57e6620e-796a-40ee-ae6e-ea1daa253b6c | cirros2 | active |
 +--------------------------------------+---------+--------+


**Related Documentation**

- Deploying Tungsten Fabric Cluster using Contrail-Command and instances.yml

.. _dependency: https://github.com/Juniper/contrail-ansible-deployer/wiki/Provisioning-F.A.Q#5-vrouter-module-is-not-getting-installed-on-the-computes-vrouter-container-in-error-state-and-docker-logs-show-the-error-like-this

.. _https://github.com/Juniper/contrail-kolla-ansible/.../globals.yml: https://github.com/Juniper/contrail-kolla-ansible/blob/contrail/ocata/etc/kolla/globals.yml

.. _https://github.com/Juniper/contrail-kolla-ansible/.../all.yml: https://github.com/Juniper/contrail-kolla-ansible/blob/contrail/ocata/ansible/group_vars/all.yml

.. _https://github.com/Juniper/contrail-container-builder/.../common.sh: https://github.com/Juniper/contrail-container-builder/blob/master/containers/base/common.sh

.. _Configuration Sample for Multi Node OpenStack HA and Tungsten Fabric (multi interface): https://github.com/Juniper/contrail-ansible-deployer/wiki/Configuration-Sample-for-Multi-Node-Openstack-HA-and-Contrail-(multi-interface)

.. _Configuration Sample for Multi Node OpenStack HA and Tungsten Fabric (multi interface).: https://github.com/Juniper/contrail-ansible-deployer/wiki/Configuration-Sample-for-Multi-Node-Openstack-HA-and-Contrail-(multi-interface)

.. _Configuration Sample for Multi Node OpenStack HA and Tungsten Fabric (single interface).: https://github.com/Juniper/contrail-ansible-deployer/wiki/Configuration-Sample-for-Multi-Node-Openstack-HA-and-Contrail-(single-interface)

.. _Configuration Sample for Multi Node OpenStack HA and Tungsten Fabric: https://github.com/Juniper/contrail-ansible-deployer/wiki/Configuration-Sample-for-Multi-Node-Openstack-HA-and-Contrail-(multi-interface)

.. _1756133: https://review.opencontrail.org/#/c/40680/
