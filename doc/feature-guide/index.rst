.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

======================
Contrail Feature Guide
======================

Overview

  Understanding Contrail Controller

    `Contrail Overview`_

    `Contrail Description`_

Installing and Upgrading Contrail

  Supported Platforms and Server Requirements

    `Supported Platforms Contrail 5.0`_

    `Server Requirements`_

  Installing Contrail and Provisioning Roles

    `Introduction to Containerized Contrail Modules`_

    `Introduction to Contrail Microservices Architecture`_

    `Downloading Installation Software`_

    `Overview of contrail-ansible-deployer for Installing Contrail with Microservices Architecture`_

    `Installing Contrail with OpenStack Ocata and Kolla Ansible`_

    `Supporting Multiple Interfaces on Servers and Nodes`_

    `Configuring the Control Node`_

    `Adding a New Node to an Existing Containerized Contrail Cluster`_

    `Using contrailctl to Configure Services Within Containers`_

    `Contrail Global Controller`_

    `Role- and Resource-Based Access Control`_

  Installation and Configuration Scenarios

    `Setting Up and Using a Simple Virtual Gateway with Contrail 4.0`_

    `Configuring MD5 Authentication for BGP Sessions`_

    `Configuring the Data Plane Development Kit (DPDK) Integrated with Contrail vRouter`_

    `Configuring Contrail DPDK vRouter to Run in a Docker Container`_

    `Configuring Single Root I/O Virtualization (SR-IOV)`_

    `Configuring Virtual Networks for Hub-and-Spoke Topology`_

    `Configuring Transport Layer Security-Based XMPP in Contrail`_

    `Configuring Graceful Restart and Long-lived Graceful Restart`_

    `Remote Compute`_

    `Dynamic Kernel Module Support (DKMS) for vRouter`_

  Using Contrail with Kubernetes

    `Contrail Integration with Kubernetes`_

    `Contrail Microservices Installation with Kubernetes`_

    `Installing and Managing Contrail 5.0 Microservices Architecture Using Helm Charts`_

    `Using Helm Charts to Provision Multinode Contrail OpenStack Ocata with High Availability`_

    `Using Helm Charts to Provision All-in-One Contrail with OpenStack Ocata`_

    `Accessing a Contrail OpenStack Helm Cluster`_

    `Frequently Asked Questions About Contrail and Helm Charts`_

    `Viewing Configuration for CNI for Kubernetes`_

    `Kubernetes Updates to IP Fabric`_

    `Implementation of Kubernetes Network Policy with Contrail Firewall Policy`_

  Using VMware vCenter with Containerized Contrail, Release 4.0.1 and Greater

    `Installing and Provisioning VMware vCenter with Containerized Contrail`_

    `Underlay Network Configuration for Containerized ContrailVM`_

    `Sample JSON Configuration Files for vCenter with Containerized Contrail 4.0.1 and Greater`_

    `Using the Contrail and VMWare vCenter User Interfaces to Manage the Network`_

    `Integrating Contrail with VMware vRealize Orchestrator`_

  Extending Contrail to Physical Routers, Bare Metal Servers, Switches, and Interfaces

    `Using ToR Switches and OVSDB to Extend the Contrail Cluster to Other Instances`_

    `Configuring High Availability for the Contrail OVSDB ToR Agent`_

    `Using Device Manager to Manage Physical Routers`_

    `SR-IOV VF as the Physical Interface of vRouter`_

    `Using Gateway Mode to Support Remote Instances`_

    `REST APIs for Extending the Contrail Cluster to Physical Routers, and Physical and Logical Interfaces`_

  Installing and Using Contrail Storage

    `Installing and Using Contrail Storage`_

  Contrail Security

    `Security Policies Draft Mode Overview`_

    `Managing Security Policies Draft Mode`_

Configuring Contrail

  Configuring Virtual Networks

    `Creating Projects in OpenStack for Configuring Tenants in Contrail`_

    `Creating a Virtual Network with Juniper Networks Contrail`_

    `Creating a Virtual Network with OpenStack Contrail`_

    `Creating an Image for a Project in OpenStack Contrail`_

    `Creating a Floating IP Address Pool`_

    `Using Security Groups with Virtual Machines (Instances)`_

    `Support for IPv6 Networks in Contrail`_

    `Configuring EVPN and VXLAN`_

  Example of Deploying a Multi-Tier Web Application Using Contrail

    `Example\:\ Deploying a Multi-Tier Web Application`_

    `Sample Network Configuration for Devices for Simple Tiered Web Application`_

  Configuring Services

    `Configuring DNS Servers`_

    `Distributed Service Resource Allocation with Containerized Contrail`_

    `Support for Multicast`_

    `Using Static Routes with Services`_

    `Configuring Metadata Service`_

  Configuring Service Chaining

    `Service Chaining`_

    `Service Chaining MX Series Configuration`_

    `ECMP Load Balancing in the Service Chain`_

    `Customized Hash Field Selection for ECMP Load Balancing`_

    `Service Chain Version 2 with Port Tuple`_

    `Using the Contrail Heat Template`_

    `Service Chain Route Reorigination`_

    `Service Instance Health Checks`_

  Examples\:\ Configuring Service Chaining

    `Example\:\ Creating an In-Network or In-Network-NAT Service Chain`_

    `Example\:\ Creating a Transparent Service Chain`_

    `Example\:\ Creating a Service Chain With the CLI`_

  Adding Physical Network Functions in Service Chains

    `Using Physical Network Functions in Contrail Service Chains`_

    `Example\:\ Adding a Physical Network Function Device to a Service Chain`_

  Configuring High Availability

    `Juniper OpenStack High Availability`_

    `High Availability Support Options`_

    `High Availability for Containerized Contrail`_

  Multitenancy Support

    `Configuring Multitenancy Support`_

    `Quality of Service in Contrail`_

    `Configuring Network QoS Parameters`_

    `BGP as a Service`_

    `BGP as a Service in Contrail Release 3.1`_

  Load Balancers

    `Using Load Balancers in Contrail`_

    `Support for OpenStack LBaaS Version 2.0 APIs`_

    `Configuring Load Balancing as a Service in Contrail`_

  Optimizing Contrail

    `Route Target Filtering`_

    `Source Network Address Translation (SNAT)`_

    `Multiqueue Virtio Interfaces in Virtual Machines`_

    `vRouter Command Line Utilities`_

Monitoring and Troubleshooting Contrail

  Configuring Traffic Mirroring to Monitor Network Traffic

    `Configuring Traffic Analyzers and Packet Capture for Mirroring`_

    `Configuring Interface Monitoring and Mirroring`_

    `Mirroring Enhancements`_

    `Analyzer Service Virtual Machine`_

    `Mapping VLAN Tags from a Physical NIC to a VMI (NIC-Assisted Mirroring)`_

  Understanding Contrail Analytics

    `Understanding Contrail Analytics`_

    `Contrail Alerts`_

    `Underlay Overlay Mapping in Contrail`_

  Configuring Contrail Analytics

    `Analytics Scalability`_

    `High Availability for Analytics`_

    `System Log Receiver in Contrail Analytics`_

    `Sending Flow Messages to the Contrail System Log`_

    `Ceilometer Support in a Contrail Cloud`_

    `User Configuration for Analytics Alarms and Log Statistics`_

    `Alarms History`_

    `Node Memory and CPU Information`_

    `Role- and Resource-Based Access Control for the Contrail Analytics API`_

    `Configuring Analytics as a Standalone Solution`_

    `Configuring Secure Sandesh and Introspect for Contrail Analytics`_

  Using Contrail Analytics to Monitor and Troubleshoot the Network

    `Monitoring the System`_

    `Debugging Processes Using the Contrail Introspect Feature`_

    `Monitor > Infrastructure > Dashboard`_

    `Monitor > Infrastructure > Control Nodes`_

    `Monitor > Infrastructure > Virtual Routers`_

    `Monitor > Infrastructure > Analytics Nodes`_

    `Monitor > Infrastructure > Config Nodes`_

    `Monitor > Networking`_

    `Query > Flows`_

    `Query > Logs`_

    `Understanding Flow Sampling`_

    `Example\:\ Debugging Connectivity Using Monitoring for Troubleshooting`_

  Common Support Answers

    `Debugging Ping Failures for Policy-Connected Networks`_

    `Debugging BGP Peering and Route Exchange in Contrail`_

    `Troubleshooting the Floating IP Address Pool in Contrail`_

    `Removing Stale Virtual Machines and Virtual Machine Interfaces`_

    `Troubleshooting Link-Local Services in Contrail`_

Contrail Commands and APIs

  Contrail Commands

    `Getting Contrail Node Status`_

    `contrail-logs (Accessing Log File Messages)`_

    `contrail-status (Viewing Node Status)`_

    `contrail-version (Viewing Version Information`_

    `service (Managing Services)`_

    `Backing Up Contrail Databases Using JSON Format`_

  Contrail Application Programming Interfaces (APIs)

    `Contrail Analytics Application Programming Interfaces (APIs) and User-Visible Entities (UVEs)`_

    `Log and Flow Information APIs`_

    `Working with Neutron`_

    `Support for Amazon VPC APIs on Contrail OpenStack`_

.. toctree::
   :maxdepth: 2
   :titlesonly:
   :glob:
   :hidden:

   overview-virtual-network-controller.rst
   components-vnc.rst
   supported-platforms-50-vnc.rst
   hardware-reqs-vnc.rst
   containers-overview.rst
   intro-microservices.rst
   download-software-vnc.rst
   install-contrail-overview-ansible-50.rst
   install-contrail-ocata-kolla-50.rst
   multi-interface-40.rst
   admin-control-node.rst
   add-node-existing-container.rst
   contrailctl.rst
   global-controller-vnc.rst
   role-resource-access-control-vmc.rst
   simple-gateway-support-vnc-40.rst
   md5-authentication-configuring.rst
   dpdk-with-vrouter-vnc-40.rst
   containerzing-contrail-dpdk-vrouter.rst
   sriov-with-vrouter-vnc.rst
   hub-spoke-vnc.rst
   config-TLS-vncDocument1.rst
   graceful-restart-bgp-persist-vnc.rst
   remote-compute-50.rst
   dkms-support-vncxml.rst
   kubernetes-cni-contrail.rst
   install-microservices-k8s.rst
   install-microsvcs-helm-chart-50.rst
   install-microsvcs-helm-multi-50.rst
   install-microsvcs-helm-aio-50.rst
   access_os_helm_cluster.rst
   install-microsvcs-helm-multi-faq-50.rst
   verifying-cni-k8s.rst
   k8s-ip-fabric.rst
   k8s-network-policy.rst
   vcenter-integration-vnc-401.rst
   vcenter-as-compute-deployment-scenarios-401.rst
   vmware-sample-json-vcenter-401.rst
   vcenter-interfaces-configuration-vnc.rst
   integrating-contrail5.0-with-vRO.rst
   using-tor-ovsdb-contrail.rst
   ha-tor-agnt.rst
   using-device-manager-netconf-contrail.rst
   sriov-phys-intf.rst
   gateway-mode-remote-instances-vnc.rst
   rest-apis-routers-contrail.rst
   storage-support-vnc-4.0.rst
   security-policy-draft-mode.rst
   security-policy-draft-mode-managing.rst
   creating-projects-vnc.rst
   creating-virtual-network-juniper-vnc.rst
   creating-virtual-network-vnc.rst
   creating-image-vnc.rst
   creating-ip-address-pool-vnc.rst
   creating-security-groups.rst
   ipv6-networks-vnc.rst
   evpn-vxlan-configuring.rst
   web-use-case-vnc.rst
   code-example-vnc.rst
   configure-dns-vnc.rst
   distributed-service-resource-allocation.rst
   broadcast-vnc.rst
   static-routes-for-services-vnc.rst
   configure-metadata-service-vnc.rst
   service-chaining-vnc.rst
   service-chaining-mx.rst
   load-balancing-vnc.rst
   custom-field-hash-vnc.rst
   service-chain-port-tuple.rst
   heat-template-vnc.rst
   service-chain-route-reorig-vnc.rst
   service-instance-health-check.rst
   service-liveness-check.rst
   bfd-health-check-vmi.rst
   bfd-health-check-bgpaas.rst
   service-health-end2end.rst
   service-instance-fate-sharing.rst
   service-chaining-example-ui.rst
   service-chaining-transparent.rst
   service-chaining-example-vnc.rst
   service-chaining-vnc-pnf.rst
   service-chaining-example-pnf.rst
   juniper-high-availability-vnc-4.0.rst
   high-avail-support-4.0.rst
   container-contrail-HA.rst
   multi-tenancy-vnc.rst
   network-qos-vnc-3.1.rst
   network-qos-configuring.rst
   bgp-as-a-service-overview.rst
   bgp-as-a-service-overview-3.1.rst
   lbaas-contrail3-F5.rst
   lbaas-v2-vnc.rst
   load-balance-as-service-vnc.rst
   route-target-filtering-vnc.rst
   snat-vnc.rst
   multiqueue-virtio-vnc.rst
   vrouter-cli-utilities-vnc.rst
   configure-traffic-analyzer-vnc.rst
   interface-monitor-mirror-vnc.rst
   mirroring-enhancements-vnc.rst
   analyzer-vm.rst
   nic-assisted-mirroring.rst
   analytics-overview-vnc.rst
   alerts-overview.rst
   underlay-overlay-mapping-vnc.rst
   analytics-scalability-vnc.rst
   ha-analytics-vnc.rst
   syslog-receiver-vnc.rst
   send-flow-msg-syslog.rst
   ceilometer-configuring.rst
   analytics-user-alarms-log-statistics.rst
   alarms-history.rst
   analytics-node-memory-cpu-info.rst
   analytics-role-resource-access-control.rst
   analytics-standalone-40-vnc.rst
   analytics-secure-sandesh-40-vnc.rst
   monitor-vnc.rst
   introspect-process-debugging.rst
   monitor-dashboard-vnc.rst
   monitoring-infrastructure-vnc.rst
   monitoring-vrouters-vnc.rst
   monitor-analytics-vnc.rst
   monitor-config-vnc.rst
   monitoring-networking-vnc.rst
   monitoring-flow-vnc.rst
   monitoring-syslog-vnc.rst
   flow-sample-overview.rst
   debug-connectivity-vnc.rst
   debug-ping-failure-vnc.rst
   debug-bgp-peering-vnc.rst
   tshoot-floating-ip-vnc.rst
   remove-stale-vms-vnc.rst
   tshoot-link-local-vnc.rst
   node-status-vnc.rst
   contrail-logs-vnc.rst
   contrail-status.rst
   contrail-version.rst
   contrail-service.rst
   backup-using-json-40.rst
   analytics-apis-vnc.rst
   analytics-apis-log-flow-vnc.rst
   neutron-perform-improve-vnc.rst
   using-vpc-vpis-vnc.rst

.. _END USER LICENSE AGREEMENT: copyright.html

.. _Table of Contents: OUTPUT-BASE-FILENAME-TOC.html

.. _About the Documentation: preface.html

.. _Documentation and Release Notes: jd0e74.html

.. _Documentation Conventions: jd0e89.html

.. _Documentation Feedback: document-feedback.html

.. _Requesting Technical Support: request-support.html

.. _Self-Help Online Tools and Resources: jd0e595.html

.. _Opening a Case with JTAC: jd0e645.html

.. _Contrail Overview: overview-virtual-network-controller.html

.. _Contrail Description: components-vnc.html

.. _Supported Platforms Contrail 5.0: supported-platforms-50-vnc.html

.. _Server Requirements: hardware-reqs-vnc.html

.. _Introduction to Containerized Contrail Modules: containers-overview.html

.. _Introduction to Contrail Microservices Architecture: intro-microservices.html

.. _Downloading Installation Software: download-software-vnc.html

.. _Overview of contrail-ansible-deployer for Installing Contrail with Microservices Architecture: install-contrail-overview-ansible-50.html

.. _Installing Contrail with OpenStack Ocata and Kolla Ansible: install-contrail-ocata-kolla-50.html

.. _Supporting Multiple Interfaces on Servers and Nodes: multi-interface-40.html

.. _Configuring the Control Node: admin-control-node.html

.. _Adding a New Node to an Existing Containerized Contrail Cluster: add-node-existing-container.html

.. _Using contrailctl to Configure Services Within Containers: contrailctl.html

.. _Contrail Global Controller: global-controller-vnc.html

.. _Role- and Resource-Based Access Control: role-resource-access-control-vmc.html

.. _Setting Up and Using a Simple Virtual Gateway with Contrail 4.0: simple-gateway-support-vnc-40.html

.. _Configuring MD5 Authentication for BGP Sessions: md5-authentication-configuring.html

.. _Configuring the Data Plane Development Kit (DPDK) Integrated with Contrail vRouter: dpdk-with-vrouter-vnc-40.html

.. _Configuring Contrail DPDK vRouter to Run in a Docker Container: containerzing-contrail-dpdk-vrouter.html

.. _Configuring Single Root I/O Virtualization (SR-IOV): sriov-with-vrouter-vnc.html

.. _Configuring Virtual Networks for Hub-and-Spoke Topology: hub-spoke-vnc.html

.. _Configuring Transport Layer Security-Based XMPP in Contrail: config-TLS-vncDocument1.html

.. _Configuring Graceful Restart and Long-lived Graceful Restart: graceful-restart-bgp-persist-vnc.html

.. _Remote Compute: remote-compute-50.html

.. _Dynamic Kernel Module Support (DKMS) for vRouter: dkms-support-vncxml.html

.. _Contrail Integration with Kubernetes: kubernetes-cni-contrail.html

.. _Contrail Microservices Installation with Kubernetes: install-microservices-k8s.html

.. _Installing and Managing Contrail 5.0 Microservices Architecture Using Helm Charts: install-microsvcs-helm-chart-50.html

.. _Using Helm Charts to Provision Multinode Contrail OpenStack Ocata with High Availability: install-microsvcs-helm-multi-50.html

.. _Using Helm Charts to Provision All-in-One Contrail with OpenStack Ocata: install-microsvcs-helm-aio-50.html

.. _Accessing a Contrail OpenStack Helm Cluster: access_os_helm_cluster.html

.. _Frequently Asked Questions About Contrail and Helm Charts: install-microsvcs-helm-multi-faq-50.html

.. _Viewing Configuration for CNI for Kubernetes: verifying-cni-k8s.html

.. _Kubernetes Updates to IP Fabric: k8s-ip-fabric.html

.. _Implementation of Kubernetes Network Policy with Contrail Firewall Policy: k8s-network-policy.html

.. _Installing and Provisioning VMware vCenter with Containerized Contrail: vcenter-integration-vnc-401.html

.. _Underlay Network Configuration for Containerized ContrailVM: vcenter-as-compute-deployment-scenarios-401.html

.. _Sample JSON Configuration Files for vCenter with Containerized Contrail 4.0.1 and Greater: vmware-sample-json-vcenter-401.html

.. _Using the Contrail and VMWare vCenter User Interfaces to Manage the Network: vcenter-interfaces-configuration-vnc.html

.. _Integrating Contrail with VMware vRealize Orchestrator: integrating-contrail5.0-with-vRO.html

.. _Using ToR Switches and OVSDB to Extend the Contrail Cluster to Other Instances: using-tor-ovsdb-contrail.html

.. _Configuring High Availability for the Contrail OVSDB ToR Agent: ha-tor-agnt.html

.. _Using Device Manager to Manage Physical Routers: using-device-manager-netconf-contrail.html

.. _SR-IOV VF as the Physical Interface of vRouter: sriov-phys-intf.html

.. _Using Gateway Mode to Support Remote Instances: gateway-mode-remote-instances-vnc.html

.. _REST APIs for Extending the Contrail Cluster to Physical Routers, and Physical and Logical Interfaces: rest-apis-routers-contrail.html

.. _Installing and Using Contrail Storage: storage-support-vnc-4.0.html

.. _Security Policies Draft Mode Overview: security-policy-draft-mode.html

.. _Managing Security Policies Draft Mode: security-policy-draft-mode-managing.html

.. _Creating Projects in OpenStack for Configuring Tenants in Contrail: creating-projects-vnc.html

.. _Creating a Virtual Network with Juniper Networks Contrail: creating-virtual-network-juniper-vnc.html

.. _Creating a Virtual Network with OpenStack Contrail: creating-virtual-network-vnc.html

.. _Creating an Image for a Project in OpenStack Contrail: creating-image-vnc.html

.. _Creating a Floating IP Address Pool: creating-ip-address-pool-vnc.html

.. _Using Security Groups with Virtual Machines (Instances): creating-security-groups.html

.. _Support for IPv6 Networks in Contrail: ipv6-networks-vnc.html

.. _Configuring EVPN and VXLAN: evpn-vxlan-configuring.html

.. _Example\:\ Deploying a Multi-Tier Web Application: web-use-case-vnc.html

.. _Sample Network Configuration for Devices for Simple Tiered Web Application: code-example-vnc.html

.. _Configuring DNS Servers: configure-dns-vnc.html

.. _Distributed Service Resource Allocation with Containerized Contrail: distributed-service-resource-allocation.html

.. _Support for Multicast: broadcast-vnc.html

.. _Using Static Routes with Services: static-routes-for-services-vnc.html

.. _Configuring Metadata Service: configure-metadata-service-vnc.html

.. _Service Chaining: service-chaining-vnc.html

.. _Service Chaining MX Series Configuration: service-chaining-mx.html

.. _ECMP Load Balancing in the Service Chain: load-balancing-vnc.html

.. _Customized Hash Field Selection for ECMP Load Balancing: custom-field-hash-vnc.html

.. _Service Chain Version 2 with Port Tuple: service-chain-port-tuple.html

.. _Using the Contrail Heat Template: heat-template-vnc.html

.. _Service Chain Route Reorigination: service-chain-route-reorig-vnc.html

.. _Service Instance Health Checks: service-instance-health-check.html

.. _Example\:\ Creating an In-Network or In-Network-NAT Service Chain: service-chaining-example-ui.html

.. _Example\:\ Creating a Transparent Service Chain: service-chaining-transparent.html

.. _Example\:\ Creating a Service Chain With the CLI: service-chaining-example-vnc.html

.. _Using Physical Network Functions in Contrail Service Chains: service-chaining-vnc-pnf.html

.. _Example\:\ Adding a Physical Network Function Device to a Service Chain: service-chaining-example-pnf.html

.. _Juniper OpenStack High Availability: juniper-high-availability-vnc-4.0.html

.. _High Availability Support Options: high-avail-support-4.0.html

.. _High Availability for Containerized Contrail: container-contrail-HA.html

.. _Configuring Multitenancy Support: multi-tenancy-vnc.html

.. _Quality of Service in Contrail: network-qos-vnc-3.1.html

.. _Configuring Network QoS Parameters: network-qos-configuring.html

.. _BGP as a Service: bgp-as-a-service-overview.html

.. _BGP as a Service in Contrail Release 3.1: bgp-as-a-service-overview-3.1.html

.. _Using Load Balancers in Contrail: lbaas-contrail3-F5.html

.. _Support for OpenStack LBaaS Version 2.0 APIs: lbaas-v2-vnc.html

.. _Configuring Load Balancing as a Service in Contrail: load-balance-as-service-vnc.html

.. _Route Target Filtering: route-target-filtering-vnc.html

.. _Source Network Address Translation (SNAT): snat-vnc.html

.. _Multiqueue Virtio Interfaces in Virtual Machines: multiqueue-virtio-vnc.html

.. _vRouter Command Line Utilities: vrouter-cli-utilities-vnc.html

.. _Configuring Traffic Analyzers and Packet Capture for Mirroring: configure-traffic-analyzer-vnc.html

.. _Configuring Interface Monitoring and Mirroring: interface-monitor-mirror-vnc.html

.. _Mirroring Enhancements: mirroring-enhancements-vnc.html

.. _Analyzer Service Virtual Machine: analyzer-vm.html

.. _Mapping VLAN Tags from a Physical NIC to a VMI (NIC-Assisted Mirroring): nic-assisted-mirroring.html

.. _Understanding Contrail Analytics: analytics-overview-vnc.html

.. _Contrail Alerts: alerts-overview.html

.. _Underlay Overlay Mapping in Contrail: underlay-overlay-mapping-vnc.html

.. _Analytics Scalability: analytics-scalability-vnc.html

.. _High Availability for Analytics: ha-analytics-vnc.html

.. _System Log Receiver in Contrail Analytics: syslog-receiver-vnc.html

.. _Sending Flow Messages to the Contrail System Log: send-flow-msg-syslog.html

.. _Ceilometer Support in a Contrail Cloud: ceilometer-configuring.html

.. _User Configuration for Analytics Alarms and Log Statistics: analytics-user-alarms-log-statistics.html

.. _Alarms History: alarms-history.html

.. _Node Memory and CPU Information: analytics-node-memory-cpu-info.html

.. _Role- and Resource-Based Access Control for the Contrail Analytics API: analytics-role-resource-access-control.html

.. _Configuring Analytics as a Standalone Solution: analytics-standalone-40-vnc.html

.. _Configuring Secure Sandesh and Introspect for Contrail Analytics: analytics-secure-sandesh-40-vnc.html

.. _Monitoring the System: monitor-vnc.html

.. _Debugging Processes Using the Contrail Introspect Feature: introspect-process-debugging.html

.. _Monitor > Infrastructure > Dashboard: monitor-dashboard-vnc.html

.. _Monitor > Infrastructure > Control Nodes: monitoring-infrastructure-vnc.html

.. _Monitor > Infrastructure > Virtual Routers: monitoring-vrouters-vnc.html

.. _Monitor > Infrastructure > Analytics Nodes: monitor-analytics-vnc.html

.. _Monitor > Infrastructure > Config Nodes: monitor-config-vnc.html

.. _Monitor > Networking: monitoring-networking-vnc.html

.. _Query > Flows: monitoring-flow-vnc.html

.. _Query > Logs: monitoring-syslog-vnc.html

.. _Understanding Flow Sampling: flow-sample-overview.html

.. _Example\:\ Debugging Connectivity Using Monitoring for Troubleshooting: debug-connectivity-vnc.html

.. _Debugging Ping Failures for Policy-Connected Networks: debug-ping-failure-vnc.html

.. _Debugging BGP Peering and Route Exchange in Contrail: debug-bgp-peering-vnc.html

.. _Troubleshooting the Floating IP Address Pool in Contrail: tshoot-floating-ip-vnc.html

.. _Removing Stale Virtual Machines and Virtual Machine Interfaces: remove-stale-vms-vnc.html

.. _Troubleshooting Link-Local Services in Contrail: tshoot-link-local-vnc.html

.. _Getting Contrail Node Status: node-status-vnc.html

.. _contrail-logs (Accessing Log File Messages): contrail-logs-vnc.html

.. _contrail-status (Viewing Node Status): contrail-status.html

.. _contrail-version (Viewing Version Information: contrail-version.html

.. _service (Managing Services): contrail-service.html

.. _Backing Up Contrail Databases Using JSON Format: backup-using-json-40.html

.. _Contrail Analytics Application Programming Interfaces (APIs) and User-Visible Entities (UVEs): analytics-apis-vnc.html

.. _Log and Flow Information APIs: analytics-apis-log-flow-vnc.html

.. _Working with Neutron: neutron-perform-improve-vnc.html

.. _Support for Amazon VPC APIs on Contrail OpenStack: using-vpc-vpis-vnc.html
