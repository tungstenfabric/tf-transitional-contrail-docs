.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==========================
Contrail Global Controller
==========================

Starting with Release 3.1, Contrail provides support for a global controller. The global controller feature provides a seamless controller experience across multiple regions in a cloud environment by helping manage multiple OpenStack installations, each having its own Keystone, Neutron, Nova and so on. High availability is provided by using separate failure domains by region.

To handle the resource burdens when connecting and configuring servers and virtual machines over multiple, different regions, the global controller has the following main responsibilities:

-  `Resource Identifier Management`_ 


-  `Multiple Location Resource Provisioning`_ 




Resource Identifier Management
--------------------------------

The global controller uses centralized resource ID management to manage multiple types of identifiers (IDs), identifying such things as route targets, virtual networks, security groups, and so on.

The Contrail global controller can interconnect virtual networks (VNs) residing in different data centers using BGP VPN technology. BGP VPN recognizes virtual private networks (VPNs) by using route target identifiers. A virtual network ID is used to identify the same virtual networks in different data centers, to prevent looping in service chains. Security group IDs identify the same security group over multiple data centers, so that the same security group policies can be used. It is important to use the same security group over multiple regions to allow traffic from all routes in the same virtual networks.

The global controller needs to manage all of the identifiers when interconnecting multiple data centers.



Multiple Location Resource Provisioning
---------------------------------------

There are many cases in which the same resource, such as policy or services, needs to exist in multiple data centers. For example, there might be a security policy to apply a firewall for any traffic for an application server network that exists in multiple locations. Each location needs to have the same virtual network, network policy, and firewalls. The Contrail global controller automates this process.



Requirements, Assumptions, and Constraints
------------------------------------------

The following are requirements, assumptions, and constraints for implementing the Contrail global controller:

- Each data center has different regions with OpenStack with Contrail.


- Each region that is managed under the same OpenStack Keystone or Keystone data must be replicated with multiple data centers.


- The global controller has a secure API connection for each OpenStack with Contrail region.


- Each Contrail controller needs peering by eBGP or iBGP; eBGP is recommended.


- Each OpenStack Keystone has an administrator account for the global controller. The account must be authorized to manage resources in each region.




Platform Support
----------------

The following are the platform requirements for the Contrail global controller:

- OpenStack Liberty


- Ubuntu 14.04.4


- Contrail Release 3.1 or greater




Installation
------------

The global controller is a new feature starting with Contrail Release 3.1. The installation instructions can be found in the following location:

https://nati.gitbooks.io/contrail-global-controller/content/doc/installation.html