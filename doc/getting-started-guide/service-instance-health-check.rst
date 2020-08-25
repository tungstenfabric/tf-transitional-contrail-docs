.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==============================
Service Instance Health Checks
==============================

In release 3.0 and greater, a service instance health check can be used to determine the liveliness of a service provided by a virtual machine (VM).

-  `Health Check Object`_ 


-  `Bidirectional Forwarding and Detection Health Check over Virtual Machine Interfaces`_ 


-  `Bidirectional Forwarding and Detection Health Check for BGPaaS`_ 


-  `Health Check of Transparent Service Chain`_ 


-  `Service Instance Fate Sharing`_ 


Health Check Object
-------------------

-  `Health Check Overview`_ 


-  `Health Check Object Configuration`_ 


-  `Creating a Health Check with the Tungsten User Interface`_ 


-  `Using the Health Check`_ 


-  `Health Check Process`_ 




Health Check Overview
---------------------

The service instance health check is used to determine the liveliness of a service provided by a VM, checking whether the service is operationally up or down. The vRouter agent uses ping and an HTTP URL to the link-local address to check the liveliness of the interface.

If the health check determines that a service is no longer operational, it removes the routes for the VM, thereby disabling packet forwarding to the VM.

The service instance health check is used with service template version 2.



Health Check Object Configuration
----------------------------------

`Table 16`_ shows the configurable properties of the health check object.

.. _Table 16: 


*Table 16* : Health Check Configurable Parameters

+--------------------+-------------------------------------------------------------------------------------------------------+
| Field              | Description                                                                                           |
+====================+=======================================================================================================+
| - enabled          | Indicates that health check is enabled. The default is **False**.                                     |
+--------------------+-------------------------------------------------------------------------------------------------------+
| - health-check-type| Indicates the health check type: **link-local, end-to-end, bgp-as-a-service**, and so on.. The default|
|                    | is link-local.                                                                                        |
+--------------------+-------------------------------------------------------------------------------------------------------+
| -monitor-type      | The protocol type to be used: **PING** or **HTTP**.                                                   |
+--------------------+-------------------------------------------------------------------------------------------------------+
| - delay            | Enter the router ID.                                                                                  |
+--------------------+-------------------------------------------------------------------------------------------------------+
| - timeout          | Enter the AS number for the node. (BGP peer only)                                                     |
+--------------------+-------------------------------------------------------------------------------------------------------+
| - max-retries      | Enter the address family, for example, **inet-vpn**.                                                  |
+--------------------+-------------------------------------------------------------------------------------------------------+
| - http-method      | BGP session hold time. The default is 90 seconds; change if needed.                                   |
+--------------------+-------------------------------------------------------------------------------------------------------+
| - url-path         | The default is 179; change if needed.                                                                 |
+--------------------+-------------------------------------------------------------------------------------------------------+
| - expected-codes   | Enable MD5 authentication if desired.                                                                 |
+--------------------+-------------------------------------------------------------------------------------------------------+




Health Check Modes
------------------

The following modes are supported for the service instance health check:

-  ``link-local`` —A local check for the service VM on the vRouter where the VM is running. In this case, the source IP of the packet is the service chain IP.


-  ``end-to-end`` —A remote address or URL is provided for a service health check through a chain of services. The destination of the health check probe is allowed to be outside the service instance. However, the health check probe must be reachable through the interface of the service instance where the health check is attached. The end-to-end health check probe is transmitted all the way to the actual destination outside the service instance. The response to the health check probe is received and processed by the service health check to evaluate the status.

Restrictions include:

 - This check is applicable for a chain where the services are not scaled out.


 - When this mode is configured, a new health check IP is allocated and used as the source IP of the packet.


 - The health check IP is allocated per ``virtual-machine-interface`` of the service VM where the health check is attached.


 - The agent relies on the ``service-health-check-ip`` flag to use as the source IP.



.. note:: In versions prior to 4.1, end-to-end health check is not supported on a transparent service chain. However, a link-local health check is possible on a transparent service instance if the corresponding service instance interface is configured with its IP address. Version 4.1 supports a segment-based health check for transparent service chain.






Creating a Health Check with the Tungsten Fabric User Interface
---------------------------------------------------------------

To create a health check with the Tungsten Fabric Web UI:


#. Navigate to **Configure > Services > Health Check Service** , and click to open the **Create** screen. See `Figure 58`_ .

			.. _Figure 58: 

			*Figure 58* : Create Health Check Screen

			.. figure:: s018766.png



#. Complete the fields to define the permissions for the health check, see `Table 17`_ .

			.. _Table 17: 


			*Table 17* : Create Health Check Fields

			+--------------------+-------------------------------------------------------------------------------------------------------+
			| Field              | Description                                                                                           |
			+====================+=======================================================================================================+
			| Name               | Enter a name for the health check service you are creating.                                           |
			+--------------------+-------------------------------------------------------------------------------------------------------+
			| Protocol           | Select from the list the protocol to use for the health check, PING, HTTP, BFD, and so on.            |
			+--------------------+-------------------------------------------------------------------------------------------------------+
			| Monitor Target     | Select fromthe list the address of the target to bemonitored by the health check.                     |
			+--------------------+-------------------------------------------------------------------------------------------------------+
			| Delay (secs)       | The delay, in seconds, to repeat the health check.                                                    |
			+--------------------+-------------------------------------------------------------------------------------------------------+
			| Timeout (secs)     | The number of seconds to wait for a response.                                                         |
			+--------------------+-------------------------------------------------------------------------------------------------------+
			| Retries            | The number of retries to attempt before declaring an instance health down.                            |
			+--------------------+-------------------------------------------------------------------------------------------------------+
			| Health Check Type  | Select from the list the type of health check—link-local, end-to-end, segment-based, bgp-as-a-service,|
			|                    | and so on.                                                                                            |
			+--------------------+-------------------------------------------------------------------------------------------------------+


Using the Health Check
----------------------

A REST API can be used to create a health check object and define its associated properties, then a link is added to the VM interface.
The health check object can be linked to multiple VM interfaces. Additionally, a VM interface can be associated with multiple health check objects. The following is an example:

::

	HealthCheckObject 1 ---------------- VirtualMachineInterface 1 ---------------- HealthCheckObject 2   
	      |  
	      |  
	VirtualMachineInterface 2 




Health Check Process
--------------------

The Tungsten Fabric vRouter agent is responsible for providing the health check service. The agent spawns a Python script to monitor the status of a service hosted on a VM on the same compute node, and the script updates the status to the vRouter agent.

The vRouter agent acts on the status provided by the script to withdraw or restore the exported interface routes. It is also responsible for providing a link-local metadata IP for allowing the script to communicate with the destination IP from the underlay network, using appropriate NAT translations. In a running system, this information is displayed in the vRouter agent introspect at:

``http://<compute-node-ip>:8085/Snh_HealthCheckSandeshReq?uuid=`` 


.. note:: Running health check creates flow entries to perform translation from underlay to overlay. Consequently, in a heavily loaded environment with a full flow table, it is possible to observe false failures.



Bidirectional Forwarding and Detection Health Check over Virtual Machine Interfaces
-----------------------------------------------------------------------------------



Release 4.1 adds support for BFD-based health checks for VMIs.

Health check for VMIs is already supported as poll-based checks with ping and curl commands. When enabled, these health checks run periodically, once every few seconds. Consequently, failure detection times can be quite large, always in seconds.

Health checks based on the BFD protocol provide failure detection and recovery in sub-second intervals, because applications are notified immediately upon BFD session state changes.


Bidirectional Forwarding and Detection Health Check for BGPaaS
--------------------------------------------------------------



Release 4.1 adds support for BFD-based health check for BGP as a Service (BGPaaS) sessions.

This health check should not be confused with the BFD-based health check over VMIs feature, also introduced in Release 4.1. The BFD-based health check for VMIs cannot be used for a BGPaaS session, because the session shares a tenant destination address over a set of VMIs, with only one VMI active at any given time.



When the BFD-based health check for BGP as a Service (BGPaaS) is configured, any time a BFD-for-BGP session is detected as down by the health-checker, corresponding logs and alarms are generated.

To enable this health check, configure the ``ServiceHealthCheckType`` property and associate it with a bgp-as-a-service configuration object. This can also be accomplished in the Tungsten Fabric Web UI.


Health Check of Transparent Service Chain
-----------------------------------------

Release 4.1 enhances service chain redundancy by implementing an end-to-end health check for the transparent service chain. The service health check monitors the status of the service chain and if there is a failure, the control node no longer considers the service chain as a valid next hop, triggering traffic failover.

A segment-based health check is used to verify the health of a single instance in a transparent service chain. The user creates a service-health-check object, with type segment-based, and attaches it to either the left or right interface of the service instance. The service health check packet is injected to the interface to which it is attached. When the packet comes out of the other interface, a reply packet is injected on that interface. If health check requests fail after 30-second retries, the service instance is considered unhealthy and the service VLAN routes of the left and right interfaces are removed. When the agent receives health check replies successfully, it adds the retracted routes back onto both interfaces, which triggers the control node to start reoriginating routes to other service instances on that service chain.

For more information, see https://github.com/Juniper/contrail-controller/blob/master/specs/transparent_sc_health_check.md 


Service Instance Fate Sharing
-----------------------------

A service chain contains multiple service instances (SI) and the failure of a single SI can cause a traffic black hole. In releases prior to Release 5.0, when an SI fails, the service chain continues to forward packets and routes reoriginate on both sides of the service chain. The packets are dropped in the SI or by the vRouter causing a black hole.

Starting in Release 5.0, when one or more than one SI in a service chain fails, reorigination of routes on both sides of the service chain is stopped and routes automatically converge to a backup service chain that is part of another Tungsten Fabric cluster. SI fate sharing brings down the service chain and the gateway nodes automatically reroutes traffic to an alternate cluster.

Starting in Release 4.1, **segment-based** health check type is used to verify the health of a SI in a service chain. To identify a failure of an SI, segment-based health check is configured either on the egress or ingress interface of the SI. When SI health check fails, the vRouter agent drops an SI route or a connected route. A connected route is also dropped if the vRouter agent restarts due to a software failure, when a compute node reboots, or when long-lived graceful restart (LLGR) is not enabled. You can detect an SI failure by keeping track of corresponding connected routes of the service chain address.


.. note:: When an SI is scaled out, the connected route for an SI interface goes down only when all associated VMs have failed.



The control node uses the  service-chain-idin  ServiceChainInfoto link all SIs in a service chain. When the control node detects that any SI of the same service-chain-id is down, it stops reoriginating routes in egress and ingress directions for all SIs. The control node reoriginates routes only when the connected routes of all the SIs are up.

