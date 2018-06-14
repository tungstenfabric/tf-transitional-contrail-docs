.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

=============================
Service Instance Fate Sharing
=============================

A service chain contains multiple service instances (SI) and the failure of a single SI can cause a traffic black hole. In releases prior to Contrail Release 5.0, when an SI fails, the service chain continues to forward packets and routes reoriginate on both sides of the service chain. The packets are dropped in the SI or by the vRouter causing a black hole.

Starting in Contrail Release 5.0, when one or more than one SI in a service chain fails, reorigination of routes on both sides of the service chain is stopped and routes automatically converge to a backup service chain that is part of another Contrail cluster. SI fate sharing brings down the service chain and the gateway nodes automatically reroutes traffic to an alternate cluster.

Starting in Contrail Release 4.1, **segment-based** health check type is used to verify the health of a SI in a service chain. To identify a failure of an SI, segment-based health check is configured either on the egress or ingress interface of the SI. When SI health check fails, the vRouter agent drops an SI route or a connected route. A connected route is also dropped if the vRouter agent restarts due to a software failure, when a compute node reboots, or when long-lived graceful restart (LLGR) is not enabled. You can detect an SI failure by keeping track of corresponding connected routes of the service chain address.


.. note:: When an SI is scaled out, the connected route for an SI interface goes down only when all associated VMs have failed.



The control node uses the  service-chain-idin  ServiceChainInfoto link all SIs in a service chain. When the control node detects that any SI of the same service-chain-id is down, it stops reoriginating routes in egress and ingress directions for all SIs. The control node reoriginates routes only when the connected routes of all the SIs are up.

