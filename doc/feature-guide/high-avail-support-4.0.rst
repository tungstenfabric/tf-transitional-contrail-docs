.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

=================================
High Availability Support Options
=================================

This section describes how to set up Contrail options for high availability support.

-  `Contrail High Availability Features`_ 


-  `Configuration Options for Enabling Contrail High Availability`_ 


-  `Supported Cluster Topologies for High Availability`_ 


-  `Deploying OpenStack and Contrail on the Same Highly Available Nodes`_ 


-  `Deploying OpenStack and Contrail on Different High Available Nodes`_ 


-  `Deploying Contrail Only on High Available Nodes`_ 




Contrail High Availability Features
-----------------------------------

The Contrail OpenStack high availability design and implementation provides:

- A high availability active-active implementation for scale-out of the cloud operation and for flexibility to expand the controller nodes to service the compute fabric.


- Anytime availability of the cloud for operations, monitoring, and workload monitoring and management.


- Self-healing of the service and states.


- VIP-based access to the cloud operations API provides an easy way to introduce new controllers and an API to the cluster with zero downtime. Improved capital efficiencies compared with dedicated hardware implementations, by using nodes assigned to controllers and making them a federated node in the cluster.


- Operational load distribution across the nodes in the cluster.


​​For more details about high availability implementation in Contrail, see `Juniper OpenStack High Availability`_ .



Configuration Options for Enabling Contrail High Availability
-------------------------------------------------------------

The following are options available to configure high availability within the Contrail configuration file ( ``testbed.py`` ).

+-----------------------------------+-----------------------------------+
| Option                            | Description                       |
+===================================+===================================+
| internal_vip                      | The virtual IP of the OpenStack   |
|                                   | high availability nodes in the    |
|                                   | control data network. In a single |
|                                   | interface setup, the internal_vip |
|                                   | will be in the management data    |
|                                   | control network.                  |
+-----------------------------------+-----------------------------------+
| external_vip                      | The virtual IP of the OpenStack   |
|                                   | high availability nodes in the    |
|                                   | management network. In a single   |
|                                   | interface setup, the              |
|                                   | external_vipis not required.      |
+-----------------------------------+-----------------------------------+
| contrail_internal_vip             | The virtual IP of the Contrail    |
|                                   | high availability nodes in the    |
|                                   | control data network. In a single |
|                                   | interface setup, the              |
|                                   | contrail_internal_vipwill be in   |
|                                   | the management data control       |
|                                   | network.                          |
+-----------------------------------+-----------------------------------+
| contrail_external_vip             | The virtual IP of the Contrail    |
|                                   | high availability nodes in the    |
|                                   | management network. In a single   |
|                                   | interface setup, the              |
|                                   | contrail_external_vipis not       |
|                                   | required.                         |
+-----------------------------------+-----------------------------------+
| nfs_server                        | The IP address of the NFS server  |
|                                   | that will be mounted to           |
|                                   | ``/var/lib/glance/images``\ fof   |
|                                   | the openstack node. The default   |
|                                   | is to env.roledefs['compute'][0]. |
+-----------------------------------+-----------------------------------+
| nfs_glance_path                   | The NFS server path to save       |
|                                   | images. The default is to         |
|                                   | ``/var/tmp/glance-images/``.      |
+-----------------------------------+-----------------------------------+
| openstack_manage_amqp             | A flag to indicate the node on    |
|                                   | which rabbitmq is set up. True    |
|                                   | indicates rabbitmq is setup on    |
|                                   | OpenStack nodes. False indicates  |
|                                   | rabbitmq is set up on OpenStack   |
|                                   | nodes and the controller          |
|                                   | container.                        |
+-----------------------------------+-----------------------------------+



Supported Cluster Topologies for High Availability
--------------------------------------------------

This section describes configurations for the cluster topologies supported, including:

- OpenStack and Contrail on the same highly available nodes


- OpenStack and Contrail on different highly available nodes


- Contrail only on highly available nodes




Deploying OpenStack and Contrail on the Same Highly Available Nodes
-------------------------------------------------------------------

OpenStack and Contrail services can be deployed in the same set of highly available nodes by setting the ``internal_vip`` parameter in the cluster configuration.
Because the high available nodes are shared by both OpenStack and Contrail services, it is sufficient to specify only ``internal_vip`` . However, if the nodes have multiple interfaces with management and data control traffic separated by provisioning multiple interfaces, then the ``external_vip`` also needs to be set in the cluster configuration.

Example
-------


::

 env.ha = {

   ‘internal_vip’ : ‘an-ip-in-control-data-network’,

   ‘external_vip’ : ‘an-ip-in-management-network’,

  }



Deploying OpenStack and Contrail on Different High Available Nodes
------------------------------------------------------------------

OpenStack and Contrail services can be deployed on different high available nodes by setting the​ ``internal_vip`` and the ``contrail_internal_vip`` parameter in the cluster configuration.
Because the OpenStack and Contrail services use different high available nodes, it is required to separately specify internal_vip for OpenStack high available nodes and contrail_internal_vip for Contrail high available nodes. If the nodes have multiple interfaces, with management and data control traffic separated by provisioning multiple interfaces, then the ``external_vip`` and ``contrail_external_vip`` options also must be set in the cluster configuration.

Example
-------


::

 env.ha = {

   ‘internal_vip’ : ‘an-ip-in-control-data-network’,

   ‘external_vip’ : ‘an-ip-in-management-network’,

   ‘contrail_internal_vip’ : ‘another-ip-in-control-data-network’,

   ‘contrail_external_vip’ : ‘another-ip-in-management-network’,

  } 

By default, the ``rabbitmq`` cluster is configured on OpenStack nodes. To manage a separate ``rabbitmq`` cluster for Contrail services, set the ``openstack_manage_amqp`` to ``false`` in the cluster configuration. In this case, OpenStack services use the ``rabbitmq`` cluster on OpenStack nodes and Contrail services use ``rabbitmq`` cluster on controller containers.

Example:
--------


::

  "openstack":{
                   "openstack_manage_amqp": false
               }



Deploying Contrail Only on High Available Nodes
-----------------------------------------------

Contrail services can be deployed only on a set of high available nodes by setting the ``contrail_internal_vip`` parameter in the cluster configuration.
Because the high available nodes are used by only Contrail services, it is sufficient to specify only ``contrail_internal_vip`` . If the nodes have multiple interfaces with management and data control traffic are separated by provisioning multiple interfaces, the ``contrail_external_vip`` also needs to be set in the cluster configuration.

Example
-------


::

 env.ha = {

   ‘contrail_internal_vip’ : ‘an-ip-in-control-data-network’,

   ‘contrail_external_vip’ : ‘an-ip-in-management-network’,

  }

By default, the ``rabbitmq`` cluster is configured on OpenStack nodes. To manage a separate ``rabbitmq`` cluster for Contrail services, set the ``openstack_manage_amqp`` to ``false`` in the cluster configuration. In this case, OpenStack services use the ``rabbitmq`` cluster on OpenStack nodes and Contrail services use ``rabbitmq`` cluster on controller containers.

Example:
--------


::

  "openstack":{
                   "openstack_manage_amqp": false
               }

**Related Documentation**

-  `Juniper OpenStack High Availability`_ 

.. _Juniper OpenStack High Availability: juniper-high-availability-vnc-4.0.html

.. _Juniper OpenStack High Availability: juniper-high-availability-vnc-4.0.html

