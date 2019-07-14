.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===========================
Tungsten Fabric Description
===========================

-  `Tungsten Fabric Major Components`_ 

-  `Tungsten Fabric Solution`_ 

Tungsten Fabric Major Components
--------------------------------

The following are the major components of Tungsten Fabric.

Tungsten Fabric Control Nodes
----------------------

- Responsible for the routing control plane, configuration management, analytics, and the user interface.


- Provide APIs to integrate with an orchestration system or a custom user interface.


- Horizontally scalable, can run on multiple servers.

Tungsten Fabric Compute Nodes – XMPP Agent and vRouter
------------------------------------------------------

- Responsible for managing the data plane.


- Functionality can reside on a host OS.

Tungsten Fabric Solution
------------------------

Tungsten Fabric architecture takes advantage of the economics of cloud computing and simplifies the physical network (IP fabric) with a software virtual network overlay that delivers service orchestration, automation, and intercloud federation for public and hybrid clouds.

Similar to the native Layer 3 designs of web-scale players in the market and public cloud providers, the Tungsten Fabric solution leverages IP as the abstraction between dynamic applications and networks, ensuring smooth migration from existing technologies, as well as support of emerging dynamic applications.

The Tungsten Fabric solution is software running on x86 Linux servers, focused on enabling multitenancy for enterprise Information Technology as a Service (ITaaS). Multitenancy is enabled by the creation of multiple distinct Layer 3-enabled virtual networks with traffic isolation, routing between tenant groups, and network-based access control for each user group. To extend the IP network edge to the hosts and accommodate virtual machine workload mobility while simplifying and automating network (re)configuration, Tungsten Fabric maintains a real-time state across dynamic virtual networks, exposes the network-as-a-service to cloud users, and enables deep network diagnostics and analytics down to the host.

In this paradigm, users of cloud-based services can take advantage of services and applications and assume that pooled, elastic resources are orchestrated, automated, and optimized across compute, storage, and network nodes in a converged architecture that is application-aware and independent of underlying hardware and software technologies.

**Related Documentation**

- `Tungsten Fabric Overview`_ 

.. _Tungsten Fabric Overview: overview-virtual-network-controller.html

