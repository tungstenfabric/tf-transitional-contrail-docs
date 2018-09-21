.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

============================================
Simple Underlay Connectivity without Gateway
============================================

-  `Simple Routing of Packets Without a Gateway`_ 


-  `Supported Use Cases`_ 


-  `Implementation: Routing Instances`_ 


-  `Implementation`_ 

Simple Routing of Packets Without a Gateway
-------------------------------------------

For simple enterprise use cases and public cloud environments, it is possible to directly route packets using the IP fabric network without using an SDN gateway.

The primary use for Contrail in this mode is to manage distributed security policy for workloads or bare metal servers.

The following features can be enabled when using this method:

- Network policy support for IP fabric


- Security groups for VMs and containers on IP fabric


- Security groups for vhost0 interface, to protect compute node or bare metal server applications


- Support for service chaining, if policy dictates that traffic goes through a service chain.




Supported Use Cases
-------------------

Starting with Contrail 4.1, the IP fabric network present in the default project can be marked for IP fabric based forwarding without tunneling. When two virtual networks with this type of configuration communicate, traffic will be forwarded directly using the underlay.

The following use cases for no SDN gateway are supported.

- Virtual networks with an IP subnet that is a subset of the IP fabric network or another subnet, and are using the IP fabric network as the provider network.

VMs and containers from this type of VNs communicate within their VNs, with IP fabric VN, and with other VNs that also have IP fabric as their provider network based on configured policy, using only the underlay, with no tunneling.


- Virtual networks with IP fabric VN as their provider network, communicating with other VNs that do not have any provider network based on policy configured, using overlay with tunneling.


- Vhost communication , with other compute vhosts and with VMs and containers in the IP fabric network or other VNs with IP fabric network as the provider network based on policy configured, using underlay and no tunneling.


- Vhost communication with VMs in any virtual network based on policy configuration, using overlay with tunneling.




Implementation: Routing Instances
---------------------------------

To implement the simple underlay connectivity with no SDN gateway, the IP fabric network has two routing instance associations:

- A default routing instance, ``ip-fabric:default`` , which is used for all forwarding decisions by the data path.


- A new routing instance, ``ip-fabric:ip-fabric`` , to carry L3VPN routes for endpoints in IP fabric. Network policy and security groups are applied based on these entries.


The IP fabric network can be associated with an IPAM and have its subnets. The IPAM for IP fabric will always use a flat subnet mode, whereby the same subnet can be shared with multiple virtual networks. The IP fabric IPAM has the overall subnet, with other virtual networks using blocks from this subnet.



IPAM Addressing Schemes
-----------------------

Two IPAM addressing schemes are supported for IP fabric:

- Common subnet mode with a set of subnet prefixes.


- Prefix per vrouter mode. To scale up underlay routing, block allocation per vrouter is supported, whereby address blocks are advertised instead of individual addresses. Every vrouter and compute node gets its own prefix. IP address-to-VMI allocation occurs after the scheduling decision is made for the VM or container. This scheme is supported for K8S and Mesos without restrictions. However, OpenStack requires the address before the scheduling decision, so in this scheme, the user must assign an address and dictate the scheduling decision to use OpenStack.

Operation
---------

When a VMI is created in the IP fabric network, the vrouter exports an L3VPN route for the VMI in the ip-fabric:ip-fabric routing instance, with the vrouter as the next hop (along with the MPLS label, policy tags, security group tags, and so on). An Inet route is exported in the ip-fabric:default routing instance, with the vrouter as next hop.

Vrouters use the ip-fabric routing instance to apply policy and the default routing instance is used to forward traffic. The control node peers with ToRs and publishes the routes of the vrouter nexthops of the TOR.

It is expected that the ToR propagates these routes to the rest of the underlay network. When using the prefix per vrouter mode, the ToR might also be configured with static routes pointing to the compute nodes, instead of peering with the control node.

Vhost interface is also added in the default routing instance. Policy and security groups can be applied on this interface as well, so that traffic from the applications and services running on the host can be subjected to all policy decisions possible in Contrail.

The IP fabric network is a Layer 3-only network and the vrouter only looks at the routing table for all forwarding decisions.



ARP Handling
------------

ARP requests in the IP fabric network and in VNs with the IP fabric network as the provider network are handled in the following ways:

- VM-to-VM communication, on the same compute or on different compute nodes— Respective vrouters respond to ARP requests from the VMs with the vrouter's MAC. Agent resolves the ARP for other compute nodes to fill the next hop corresponding to remote VMs.


- Vhost connectivity to VM on the same compute node—Vrouter responds with vhost MAC (its own MAC) for ARP requests from vhost. ARP requests from the VM will be responded with vrouter's MAC.


Each subnet in the networks, IP fabric network or other VNs using IP fabric as the provider network, has a subnet route in the compute host pointing to the vhost interface. There is a Layer 3 route in the fabric default VRF for each VM, with the next hop pointing to its VMI. Traffic is forwarded to the VM based on this route. The next hop is a Layer 3 interface next hop with the source MAC being the vrouter’s MAC.

When the vhost and the VN are using different subnets, an ARP request from the vhost has the VM's IP as the destination IP and the vhost’s IP as the source IP. Vrouter responds to an ARP request with the vhost’s MAC.

- Vhost connectivity to VM on a different compute node—ARP requests for VMs on a different compute node are flooded on the fabric interface. The compute node hosting the VM has a Layer 3 route for the VM, with the next hop pointing to its VMI. The vrouter on that node responds to the ARP request with its vhost MAC address. The VM’s ARP request is always responded to by with vrouter’s MAC.


- Vhost connectivity to another compute node—As in the previous example, the ARP request is transmitted on the fabric interface. Other vrouters cross connect the ARP request to their vhost interface because there is not any Layer 3 route pointing to the VMI. The host responds to the ARP request.


Broadcast and Multicast Traffic
-------------------------------

In Contrail 4.1, broadcast or multicast traffic from VMs in the IP fabric network and from VNs having IP fabric network as the provider network is handled in the normal way, using the native routing instance of the interface from which it originates.. DHCP requests from these VMs are served by the vrouter agent.

Implementation
--------------

A virtual network can have a provider network configured using a link from the VN to the IP fabric VN.

A vrouter-specific IP allocation pool can be created. If an instance IP is created with a link to a vrouter and the vrouter is linked with a flat subnet IPAM, then the instance IP is allocated an address from the vrouter-specific allocation pool.

Provisioning will create VMI for vhost interface. Creation of virtual networks with IP fabric forwarding, policy / security group configurations for vhost interface can now be done.

