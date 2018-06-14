.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===============================
Kubernetes Updates to IP Fabric
===============================

This topic describes the updates to Kubernetes and supported features in Contrail Release 5.0:

-  `Reachability to Kubernetes Pods Using the IP Fabric Forwarding Feature`_ 


-  `Service Isolation Through Virtual Networks`_ 


-  `Contrail ip-fabric-snat Feature`_ 


-  `Third-Party Ingress Controllers`_ 


-  `Custom Network Support for Ingress Resources`_ 


-  `Kubernetes Probes and Kubernetes Service Node-Port`_ 


-  `Kubernetes 1.9 Network-Policy Support`_ 




Reachability to Kubernetes Pods Using the IP Fabric Forwarding Feature
----------------------------------------------------------------------

A Kubernetes pod is a group of one or more containers (such as Docker containers), the shared storage for those containers, and options on how to run the containers. Since pods are in the overlay network, they cannot be reached directly from the underlay without a gateway or vRouter. In Contrail Release 5.0, the IP fabric forwarding (  ip-fabric-forwarding) feature enables virtual networks to be created as part of the underlay network and eliminates the need for encapsulation and decapsulation of data. The ip-fabric-forwarding feature is only applicable for pod networks. If  ip-fabric-forwardingis enabled, pod-networks are associated to ip-fabric-ipam instead of pod-ipam which is also a flat subnet.


*Reviewer:* Is ip-fabric-ipam a flat subnet or is pod-ipam a flat subnet? What is the advantage of this being a flat subnet\?\`

The ip-fabric-forwarding feature is enabled and disabled in the global and namespace levels. By default,  ip-fabric-forwardingis disabled in the global level. To enable it in global level, you must set  “ip_fabric_forwarding”to  “true”in the  “[KUBERNETES]”section of the ``/etc/contrail/contrail-kubernetes.conf`` file. To enable or disable the feature in namespace level, you must set  “ip_fabric_forwarding”to  “true”or  “false”respectively in namespace annotation. For example,  “opencontrail.org/ip_fabric_forwarding”: “true”. Once the feature is enabled, it cannot be disabled.

*Reviewer:* If the feature is enabled, can it not be disabled in both global and namespace levels?

For more information, see `Gateway-less Forwarding`_  .



Service Isolation Through Virtual Networks
------------------------------------------

In namespace isolation mode, services in one namespace are not accessible from other namespaces, unless security groups or network policies are explicitly defined to allow access. If any Kubernetes service is implemented by pods in an isolated namespace, those services are reachable only to pods in the same namespace through the Kubernetes  service-ip.

The Kubernetes  service-ipis allocated from the cluster network despite being in an isolated namespace. So, by default, service from one namespace can reach services from another namespace. However, security groups in isolated namespaces prevent reachability from external namespace and also prevent reachability from outside of the cluster. In order to enable access by external namespaces, the security group must be edited to allow access to all namespaces which defeats the purpose of isolation.

Contrail Release 5.0 enables service or ingress reachability from external clusters in isolated namespaces. Two virtual networks are created in isolated namespaces. One network is dedicated to pods and one is dedicated to services. Contrail network-policy is created between the pod network and the service network for reachability between pods and services. Service uses the same service-ipam which is a flat-subnet like pod-ipam. It is applicable for default namespace as well.

*Reviewer:* What is applicable for default namespace as well?

*Reviewer:* Again, what is the advantage of service-ipam being a flat subnet?



Contrail ip-fabric-snat Feature
-------------------------------
*Reviewer:* What is the benefit of this feature? We know what it does but not why we need it.

With the Contrail ip-fabric-snat feature, pods that are in the overlay can reach the Internet without floating IPs or a logical-router. The ip-fabric-snat feature uses compute node IP for creating a source NAT to reach the required services and is applicable only to pod networks. The kube-manager reserves ports 56000 through 57023 for TCP and 57024 through 58047 for UDP to create a source NAT in global-config during the initialization.

The ip-fabric-snat feature can be enabled or disabled in the global or namespace levels. By default, the feature is disabled in the global level. To enable the ip-fabric-snat feature in the global level, you must set  “ip-fabric-snat”to  “true”in the  “[KUBERNETES]”section in the ``/etc/contrail/contrail-kubernetes.conf`` file. To enable or disable it in the namespace level, you must set  “ip_fabric_snat”to  “true”or  “false”respectively in namespace annotation. For example,  “opencontrail.org/ip_fabric_snat”: “true”. The ip_fabric_snat feature can be at enabled and disabled any time. To enable or disable the ip_fabric_snat feature in the default-pod-network, default namespace must be used. If the  ip_fabric_forwardingis enabled,  ip_fabric_snatis ignored.

For more information, see `Distributed SNAT`_  .



Third-Party Ingress Controllers
-------------------------------

Multiple ingress controllers can co-exist in Contrail. If  “kubernetes.io/ingress.class”is absent or is  “opencontrail”in the annotations of the Kubernetes ingress resource, the kube-manager creates a HAProxy loadbalancer. Otherwise it is ignored and the respective ingress controller handles the ingress resource. Since Contrail ensures the reachability between pods and services, any ingress controller can reach the endpoints or pods directly or through services.

*Reviewer:* “Otherwise it is ignore”. What is ignored? The kube-manager?


Custom Network Support for Ingress Resources
--------------------------------------------

Contrail supports custom networks in namespace level for pods. Starting with Contrail Release 5.0, custom networks are supported for ingress resources as well.



Kubernetes Probes and Kubernetes Service Node-Port
--------------------------------------------------

The Kubelet needs reachability to pods for liveness and readiness probes. Contrail network policy is created between the IP fabric network and pod network to provide reachability between node and pods. Whenever the pod network is created, the network policy is attached to the pod network to provide reachability between node and pods. So, any process in the node can reach the pods.

Kubernetes Service Node-Port is based on node reachability to pods. Since Contrail provides connectivity between node and pods through Contrail the network policy, Node Port is supported.



Kubernetes 1.9 Network-Policy Support
--------------------------------------

Contrail Release 5.0 supports implementing Kubernetes network policy in Contrail using the Contrail firewall security policy framework. While Kubernetes network policy can be implemented using other security objects in Contrail like security groups and Contrail network policies, the support of tags by Contrail firewall security policy aids in the simplification and abstraction of workloads.

For more information, see `Implementation of Kubernetes Network Policy with Contrail Firewall Policy`_ .

**Related Documentation**

-  `Implementation of Kubernetes Network Policy with Contrail Firewall Policy`_ 

-  `Contrail Integration with Kubernetes`_ 

.. _Implementation of Kubernetes Network Policy with Contrail Firewall Policy: k8s-network-policy.html

.. _Implementation of Kubernetes Network Policy with Contrail Firewall Policy: k8s-network-policy.html

.. _Contrail Integration with Kubernetes: kubernetes-cni-contrail.html


.. _Gateway-less Forwarding: https://github.com/Juniper/contrail-specs/blob/master/gateway-less-forwarding.md

.. _Distributed SNAT: https://github.com/Juniper/contrail-specs/blob/master/distributed-snat.md
