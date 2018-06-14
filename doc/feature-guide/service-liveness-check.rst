.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===================
Health Check Object
===================

   -  `Health Check Overview`_ 


   -  `Health Check Object Configuration`_ 


   -  `Creating a Health Check with the Contrail User Interface`_ 


   -  `Using the Health Check`_ 


   -  `Health Check Process`_ 




Health Check Overview
---------------------

The service instance health check is used to determine the liveliness of a service provided by a VM, checking whether the service is operationally up or down. The vRouter agent uses ping and an HTTP URL to the link-local address to check the liveliness of the interface.

If the health check determines that a service is no longer operational, it removes the routes for the VM, thereby disabling packet forwarding to the VM.

The service instance health check is used with service template version 2.



Health Check Object Configuration
----------------------------------

 `Table 21`_ shows the configurable properties of the health check object.

    .. _Table 21: 


   *Table 21* : Health Check Configurable Parameters



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



.. note:: In versions prior to Contrail 4.1, end-to-end health check is not supported on a transparent service chain. However, a link-local health check is possible on a transparent service instance if the corresponding service instance interface is configured with its IP address. Contrail 4.1 supports a segment-based health check for transparent service chain.






Creating a Health Check with the Contrail User Interface
--------------------------------------------------------

To create a health check with the Contrail Web UI:


#. Navigate to **Configure > Services > Health Check Service** , and click to open the **Create** screen. See `Figure 95`_ .

   .. _Figure 95: 

     *Figure 95* : Create Health Check Screen

    .. figure:: s018766.png



#. Complete the fields to define the permissions for the health check, see `Table 22`_ .

    .. _Table 22: 


   *Table 22* : Create Health Check Fields




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

The Contrail vRouter agent is responsible for providing the health check service. The agent spawns a Python script to monitor the status of a service hosted on a VM on the same compute node, and the script updates the status to the vRouter agent.

The vRouter agent acts on the status provided by the script to withdraw or restore the exported interface routes. It is also responsible for providing a link-local metadata IP for allowing the script to communicate with the destination IP from the underlay network, using appropriate NAT translations. In a running system, this information is displayed in the vRouter agent introspect at:

 ``http:// *<compute-node-ip>* :8085/Snh_HealthCheckSandeshReq?uuid=`` 


.. note:: Running health check creates flow entries to perform translation from underlay to overlay. Consequently, in a heavily loaded environment with a full flow table, it is possible to observe false failures.



