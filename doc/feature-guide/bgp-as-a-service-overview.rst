.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

=================
BGP as a Service
=================

The BGP as a Service (BGPaaS) feature allows a guest virtual machine (VM) to place routes in its own virtual routing and forwarding (VRF) instance using BGP.

-  `Contrail BGPaaS Features`_ 


-  `BGPaaS Customer Use Cases`_ 


-  `Configuring BGPaaS`_ 




Contrail BGPaaS Features
------------------------

Using BGPaaS with Contrail requires the guest VM to have connectivity to the control node and to be able to advertise routes into the VRF instance.

With the BGPaaS feature:

- The vRouter agent is able to accept BGP connections from the VMs and proxy them to the control node.


- The vRouter agent always selects one of the control nodes that it is using as an XMPP server.


Starting with Contrail Release 3.0, the following features have been added to BGPaaS:

- All BGPaaS sessions are configured to have bidirectional exchange of routes.


- If inet6 routes are being advertised to the tenant VM, they are advertised with the IPv6 subnet's default gateway address as the BGP next hop.


- If multiple tenant VMs in the same virtual network have BGPaaS sessions and they use eBGP, standard loop prevention rules prevent routes advertised by one tenant VM from being advertised to other tenant VMs


A second BGP session for high availability can also be configured appropriately using one more BGP router object in the Contrail configuration and the peering session (from the VNF’s point of view) to the DNS IP address (reserved by Contrail).

The following are caveats:

- BGP sessions must use IPv4 transport.


- The VNF must support RFC 2545, *Use of BGP-4 Multiprotocol Extensions for IPv6 Inter-Domain Routing* , to carry IPv6 routes over the IPv4 peer.


- Only IPv4 (inet) and IPv6 (inet6) address families are supported.


The initial implementation of BGPaaS Version 1, supported in Contrail Release 3.0, allowed a tenant VM to establish BGP sessions to the default gateway and DNS server in the VM’s subnet. A limitation of this implementation was that the tenant VM could advertise routes into the virtual network to which the VM belonged, however, the VM could not receive any routes. The tenant VM was required to use a static default route, with the subnet's default gateway as the next hop.

Contrail Release 3.1 eliminates the previous limitation and provides route export functionality for BGPaaS sessions. The next hop for all routes advertised to the tenant VM is set to the default gateway address of the subnet of the tenant VM. This allows the tenant BGP implementation to be relatively simple, by not requiring support for recursive resolution of BGP next hops.

The BGPaaS object is associated with a virtual machine interface (VMI), not just a virtual machine (VM), which enables a tenant VM to have BGP sessions in multiple virtual networks, if required.

Starting with Contrail Release 3.1, the following features and properties have been added to BGPaaS:

- By default, all BGPaaS sessions are configured to have bidirectional exchange of routes. The Boolean property  bgpaas-suppress-route-advertisementensures no advertisement of routes to the tenant VM.


- If inet6 routes are being advertised to the tenant VM, they are advertised with the IPv6 subnet's default gateway address as the BGP next hop. A Boolean property,  bgpaas-ipv4-mapped-ipv6-nexthop, causes the IPv4 subnet's default gateway, in IPv4-mapped IPv6 format, to be used instead as the next hop.


- If multiple tenant VMs in the same virtual network have BGPaaS sessions and they use eBGP, the standard BGP AS path loop prevention rules prevent routes advertised by one tenant VM from being advertised to the other tenant VMs. The  as-overridefield, added to the existing ``BgpSessionAttributes`` in the BGPaaS object, causes the control node to replace the AS number of the tenant VM with it's own AS number, when advertising routes learned from a tenant VM to another tenant VM in the same virtual network. The tenant VM does not need to implement any new functionality.




BGPaaS Customer Use Cases
-------------------------

This section provides example scenarios for implementing BGPaaS with Contrail.

-  `Dynamic Tunnel Insertion Within a Tenant Overlay`_ 


-  `Dynamic Network Reachability of Applications`_ 


-  `Liveness Detection for High Availability`_ 


Dynamic Tunnel Insertion Within a Tenant Overlay
------------------------------------------------

Various applications need to insert dynamic tunnels into virtual networks. Virtual network functions (VNFs) provide the function of tunnel termination. Tunnel termination types vary across application types, such as business VPN, mobility small site backhaul, VPC, and the like. The key requirement is that tunnels need to insert dynamically new network reachability information into the virtual network. The predominant methods of tunnel network reachability insertion use BGP.

BGPaaS allows the migration of brownfield VNFs into Contrail, preserving the application behavior and requirement for BGP, without rewriting the application.

The following figure is a generic example showing the need to insert a dynamic tunnel into a virtual network.


.. figure:: S018554.png



Dynamic Network Reachability of Applications
--------------------------------------------

The Domain Name System (DNS) is a widespread application that uses BGP as a mechanism to tune reachability of its services, based on metrics such as load, maintenance, availability, and the like. As DNS services are migrated to environments using overlays, a mechanism to preserve the existing application behavior and requirements is needed, including the ability to announce and withdraw reachability to the available application.

This requirement is not limited to DNS. Other applications, such as virtualized evolved packet core (vEPC) and others, use BGP as a mechanism for network reachability based on availability and load.



Liveness Detection for High Availability
----------------------------------------

Various keepalive mechanisms for tenant reachability have been provided by network components such as BGP, OSPF, PING, VRRP, BFD, or application-specific mechanisms. With BGP on the vRouter agent, BGP can be used to provide a liveness detection mechanism between the tenant on the local compute node and the services that the specific tenant VM is providing.



Configuring BGPaaS
------------------

The following are methods for configuring BGPaaS:

-  `Configuring BGPaaS Using VNC API`_ 


-  `Using the Contrail User Interface to Configure BGPaaS`_ 




Configuring BGPaaS Using VNC API
--------------------------------

To use VNC APIs to configure BGPaaS:




#. Access the default project.

   ``default_project = self._vnc_lib.project_read(fq_name=[u'default-domain', ‘bgpaas-tenant’])`` 



#. Create a BGPaaS object.

   ``bgpaas_obj = BgpAsAService(name=‘bgpaas_1’, parent_obj=default_project)`` 



#. Attach the BGP object to a precreated VMI.

   ``bgpaas_obj.add_virtual_machine_interface(vmi)`` 



#. Set the ASN. It must be an eBGP session.

   ``bgpaas_obj.set_autonomous_system('65000')`` 

   If the ASN is not set, the primary instance IP will be chosen.

   ``bgpaas_obj.set_bgpaas_ip_address(u’10.1.1.5’)`` 



#. Set session attributes.

   ``bgp_addr_fams = AddressFamilies(['inet’, ‘inet6’])bgp_sess_attrs = BgpSessionAttributes(address_families=bgp_addr_fams,hold_time=60)bgpaas_obj.set_bgpaas_session_attributes(bgp_sess_attrs)self._vnc_lib.bgp_as_a_service_create(bgpaas_obj)`` 




Deleting a BGPaaS Object
------------------------

To delete a BGPaaS object:

``fq_name=[u'default-domain', ‘bgpaas-tenant’, ‘bgpaas_1’]bgpaas_obj = self._vnc_lib.bgp_as_a_service_read(fq_name=fq_name)bgpaas_obj.del_virtual_machine_interface(vmi)self._vnc_lib.bgp_as_a_service_update(bgpaas_obj)self._vnc_lib.bgp_as_a_service_delete(id=bgpaas_obj.get_uuid())`` 



Using the Contrail User Interface to Configure BGPaaS
-----------------------------------------------------

To configure BGPaaS within a tenant:


#. Within a tenant in Contrail, navigate to **Configure > Services > BGP as a Service** . Select the + icon to access the window **Create BGP as a Service** .


   .. figure:: S018555.png



#. Enter the relevant information at the **Create BGP as a Service** window, including ASN, address family, and VMI identification.



#. Click **Save** to create the BGP object.


