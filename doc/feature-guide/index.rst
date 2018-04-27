

======================
Contrail Feature Guide
======================

Overview

  Understanding Contrail Controller

    `Contrail Overview`_

    `Contrail Description`_

    `Contrail Installation Overview`_

Installing and Upgrading Contrail

  Supported Platforms and Server Requirements

    `Supported Platforms Contrail 4.1`_

    `Server Requirements`_

  Installing Contrail and Provisioning Roles

    `Introduction to Containerized Contrail Modules`_

    `Downloading Installation Software`_

    `Installing the Operating System and Contrail Packages`_

    `Installing Containerized Contrail Clusters Using Server Manager`_

    `Installing Containerized Contrail Using Server Manager Lite (SM-Lite)`_

    `Supporting Multiple Interfaces on Servers and Nodes`_

    `Configuring the Control Node`_

    `Adding a New Node to an Existing Containerized Contrail Cluster`_

    `Using contrailctl to Configure Services Within Containers`_

    `Supporting Multiple Interfaces on Servers and Nodes`_

    `Contrail Global Controller`_

    `Role- and Resource-Based Access Control`_

  Installation and Configuration Scenarios

    `Setting Up and Using a Simple Virtual Gateway with Contrail 4.0`_

    `Simple Underlay Connectivity without Gateway`_

    `Configuring MD5 Authentication for BGP Sessions`_

    `Configuring the Data Plane Development Kit (DPDK) Integrated with Contrail vRouter`_

    `Configuring Single Root I/O Virtualization (SR-IOV)`_

    `Provisioning DPDK SRIOV with Server Manager`_

    `Configuring Virtual Networks for Hub-and-Spoke Topology`_

    `Configuring Transport Layer Security-Based XMPP in Contrail`_

    `Configuring Graceful Restart and Long-lived Graceful Restart`_

  Using Contrail with Kubernetes

    `Contrail Integration with Kubernetes`_

    `Installing and Provisioning Containerized Contrail Controller for Kubernetes`_

    `Viewing Configuration for CNI for Kubernetes`_

    `Provisioning Contrail CNI for Kubernetes`_

    `Using Kubernetes Helm to Provision Contrail`_

  Using VMware vCenter with Containerized Contrail, Release 4.0.1 and Greater

    `Installing and Provisioning VMware vCenter with Containerized Contrail`_

    `Underlay Network Configuration for Containerized ContrailVM`_

    `Sample JSON Configuration Files for vCenter with Containerized Contrail 4.0.1 and Greater`_

    `Using the Contrail and VMWare vCenter User Interfaces to Manage the Network`_

  Using Contrail with Red Hat

    `Deploying Contrail with Red Hat OpenStack Platform Director 10`_

    `Installing Red Hat OpenShift Container Platform with Contrail Networking`_

    `Upgrade Procedure for RHOSP-based Contrail 3.2.x to Contrail 4.1`_

    `Restoring Contrail Nodes in a RHOSP-based Environment`_

  Using Server Manager to Automate Provisioning

    `Installing Server Manager`_

    `Using Server Manager to Automate Provisioning`_

    `Using the Server Manager Web User Interface`_

    `Installing and Using Server Manager Lite`_

  Extending Contrail to Physical Routers, Bare Metal Servers, Switches, and Interfaces

    `Using ToR Switches and OVSDB to Extend the Contrail Cluster to Other Instances`_

    `Configuring High Availability for the Contrail OVSDB ToR Agent`_

    `Using Device Manager to Manage Physical Routers`_

    `SR-IOV VF as the Physical Interface of vRouter`_

    `Using Gateway Mode to Support Remote Instances`_

    `REST APIs for Extending the Contrail Cluster to Physical Routers, and Physical and Logical Interfaces`_

  Installing and Using Contrail Storage

    `Installing and Using Contrail Storage`_

  Upgrading Contrail Software

    `Upgrading Contrail 4.0 to 4.1`_

    `Dynamic Kernel Module Support (DKMS) for vRouter`_

Configuring Contrail

  Configuring Virtual Networks

    `Creating Projects in OpenStack for Configuring Tenants in Contrail`_

    `Creating a Virtual Network with Juniper Networks Contrail`_

    `Creating a Virtual Network with OpenStack Contrail`_

    `Creating an Image for a Project in OpenStack Contrail`_

    `Creating a Floating IP Address Pool`_

    `Using Security Groups with Virtual Machines (Instances)`_

    `Security Policy Enhancements`_

    `Support for IPv6 Networks in Contrail`_

    `Configuring EVPN and VXLAN`_

    `EVPN-VXLAN Support for Bare Metal Devices and QFX Device Configuration`_

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

  Examples: Configuring Service Chaining

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

    `Role-Based Access Control for Analytics`_

    `System Log Receiver in Contrail Analytics`_

    `Sending Flow Messages to the Contrail System Log`_

    `More Efficient Flow Queries`_

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


.. _: OUTPUT-BASE-FILENAME-title.html

.. _END USER LICENSE AGREEMENT: copyright.html

.. _Table of Contents: OUTPUT-BASE-FILENAME.html

.. _Contrail Overview: topic-79599.html

.. _Contrail Description: topic-79661.html

.. _Contrail Installation Overview: topic-122984.html

.. _Supported Platforms Contrail 4.1: topic-122281.html

.. _Server Requirements: topic-83309.html

.. _Introduction to Containerized Contrail Modules: topic-119276.html

.. _Downloading Installation Software: topic-83311.html

.. _Installing the Operating System and Contrail Packages: topic-120313.html

.. _Installing Containerized Contrail Clusters Using Server Manager: topic-119335.html

.. _Installing Containerized Contrail Using Server Manager Lite (SM-Lite): topic-119818.html

.. _Supporting Multiple Interfaces on Servers and Nodes: topic-120314.html

.. _Configuring the Control Node: topic-79626.html

.. _Adding a New Node to an Existing Containerized Contrail Cluster: topic-120663.html

.. _Using contrailctl to Configure Services Within Containers: topic-119482.html

.. _Supporting Multiple Interfaces on Servers and Nodes: topic-120314.html

.. _Contrail Global Controller: topic-108697.html

.. _Role- and Resource-Based Access Control: topic-98751.html

.. _Setting Up and Using a Simple Virtual Gateway with Contrail 4.0: topic-120360.html

.. _Simple Underlay Connectivity without Gateway: topic-122368.html

.. _Configuring MD5 Authentication for BGP Sessions: topic-101371.html

.. _Configuring the Data Plane Development Kit (DPDK) Integrated with Contrail vRouter: topic-120361.html

.. _Configuring Single Root I/O Virtualization (SR-IOV): topic-104170.html

.. _Provisioning DPDK SRIOV with Server Manager: topic-124946.html

.. _Configuring Virtual Networks for Hub-and-Spoke Topology: topic-104185.html

.. _Configuring Transport Layer Security-Based XMPP in Contrail: topic-104237.html

.. _Configuring Graceful Restart and Long-lived Graceful Restart: topic-116509.html

.. _Contrail Integration with Kubernetes: topic-119646.html

.. _Installing and Provisioning Containerized Contrail Controller for Kubernetes: topic-120911.html

.. _Viewing Configuration for CNI for Kubernetes: topic-120581.html

.. _Provisioning Contrail CNI for Kubernetes: topic-123086.html

.. _Using Kubernetes Helm to Provision Contrail: topic-123087.html

.. _Installing and Provisioning VMware vCenter with Containerized Contrail: topic-122501.html

.. _Underlay Network Configuration for Containerized ContrailVM: topic-122503.html

.. _Sample JSON Configuration Files for vCenter with Containerized Contrail 4.0.1 and Greater: topic-122504.html

.. _Using the Contrail and VMWare vCenter User Interfaces to Manage the Network: topic-99640.html

.. _Deploying Contrail with Red Hat OpenStack Platform Director 10: topic-121428.html

.. _Installing Red Hat OpenShift Container Platform with Contrail Networking: topic-125757.html

.. _Upgrade Procedure for RHOSP-based Contrail 3.2.x to Contrail 4.1: topic-126510.html

.. _Restoring Contrail Nodes in a RHOSP-based Environment: topic-125524.html

.. _Installing Server Manager: topic-120557.html

.. _Using Server Manager to Automate Provisioning: topic-92560.html

.. _Using the Server Manager Web User Interface: topic-96137.html

.. _Installing and Using Server Manager Lite: topic-120572.html

.. _Using ToR Switches and OVSDB to Extend the Contrail Cluster to Other Instances: topic-97450.html

.. _Configuring High Availability for the Contrail OVSDB ToR Agent: topic-100807.html

.. _Using Device Manager to Manage Physical Routers: topic-97451.html

.. _SR-IOV VF as the Physical Interface of vRouter: topic-108669.html

.. _Using Gateway Mode to Support Remote Instances: topic-113610.html

.. _REST APIs for Extending the Contrail Cluster to Physical Routers, and Physical and Logical Interfaces: topic-97453.html

.. _Installing and Using Contrail Storage: topic-120484.html

.. _Upgrading Contrail 4.0 to 4.1: topic-123530.html

.. _Dynamic Kernel Module Support (DKMS) for vRouter: topic-92319.html

.. _Creating Projects in OpenStack for Configuring Tenants in Contrail: topic-79632.html

.. _Creating a Virtual Network with Juniper Networks Contrail: topic-80269.html

.. _Creating a Virtual Network with OpenStack Contrail: topic-79633.html

.. _Creating an Image for a Project in OpenStack Contrail: topic-79857.html

.. _Creating a Floating IP Address Pool: topic-79636.html

.. _Using Security Groups with Virtual Machines (Instances): topic-83128.html

.. _Security Policy Enhancements: topic-122570.html

.. _Support for IPv6 Networks in Contrail: topic-95392.html

.. _Configuring EVPN and VXLAN: topic-87215.html

.. _EVPN-VXLAN Support for Bare Metal Devices and QFX Device Configuration: topic-122696.html

.. _Example\:\ Deploying a Multi-Tier Web Application: topic-79672.html

.. _Sample Network Configuration for Devices for Simple Tiered Web Application: topic-81781.html

.. _Configuring DNS Servers: topic-79639.html

.. _Distributed Service Resource Allocation with Containerized Contrail: topic-119214.html

.. _Support for Multicast: topic-79640.html

.. _Using Static Routes with Services: topic-87798.html

.. _Configuring Metadata Service: topic-87809.html

.. _Service Chaining: topic-79680.html

.. _Service Chaining MX Series Configuration: topic-83327.html

.. _ECMP Load Balancing in the Service Chain: topic-79682.html

.. _Customized Hash Field Selection for ECMP Load Balancing: topic-104207.html

.. _Service Chain Version 2 with Port Tuple: topic-108874.html

.. _Using the Contrail Heat Template: topic-95314.html

.. _Service Chain Route Reorigination: topic-104530.html

.. _Service Instance Health Checks: topic-123257.html

.. _Example\:\ Creating an In-Network or In-Network-NAT Service Chain: topic-83168.html

.. _Example\:\ Creating a Transparent Service Chain: topic-83385.html

.. _Example\:\ Creating a Service Chain With the CLI: topic-80966.html

.. _Using Physical Network Functions in Contrail Service Chains: topic-103925.html

.. _Example\:\ Adding a Physical Network Function Device to a Service Chain: topic-103918.html

.. _Juniper OpenStack High Availability: topic-120287.html

.. _High Availability Support Options: topic-120289.html

.. _High Availability for Containerized Contrail: topic-119483.html

.. _Configuring Multitenancy Support: topic-83159.html

.. _Quality of Service in Contrail: topic-111240.html

.. _Configuring Network QoS Parameters: topic-93701.html

.. _BGP as a Service: topic-103732.html

.. _BGP as a Service in Contrail Release 3.1: topic-113557.html

.. _Using Load Balancers in Contrail: topic-103986.html

.. _Support for OpenStack LBaaS Version 2.0 APIs: topic-108720.html

.. _Configuring Load Balancing as a Service in Contrail: topic-94398.html

.. _Route Target Filtering: topic-92801.html

.. _Source Network Address Translation (SNAT): topic-92919.html

.. _Multiqueue Virtio Interfaces in Virtual Machines: topic-108731.html

.. _vRouter Command Line Utilities: topic-92800.html

.. _Configuring Traffic Analyzers and Packet Capture for Mirroring: topic-80874.html

.. _Configuring Interface Monitoring and Mirroring: topic-87848.html

.. _Mirroring Enhancements: topic-116510.html

.. _Analyzer Service Virtual Machine: topic-83226.html

.. _Mapping VLAN Tags from a Physical NIC to a VMI (NIC-Assisted Mirroring): topic-120913.html

.. _Understanding Contrail Analytics: topic-82959.html

.. _Contrail Alerts: topic-103179.html

.. _Underlay Overlay Mapping in Contrail: topic-99246.html

.. _Analytics Scalability: topic-82506.html

.. _High Availability for Analytics: topic-87847.html

.. _Role-Based Access Control for Analytics: topic-123464.html

.. _System Log Receiver in Contrail Analytics: topic-93854.html

.. _Sending Flow Messages to the Contrail System Log: topic-108670.html

.. _More Efficient Flow Queries: topic-122665.html

.. _Ceilometer Support in a Contrail Cloud: topic-100943.html

.. _User Configuration for Analytics Alarms and Log Statistics: topic-113489.html

.. _Alarms History: topic-119794.html

.. _Node Memory and CPU Information: topic-113578.html

.. _Role- and Resource-Based Access Control for the Contrail Analytics API: topic-113579.html

.. _Configuring Analytics as a Standalone Solution: topic-120833.html

.. _Configuring Secure Sandesh and Introspect for Contrail Analytics: topic-120834.html

.. _Monitoring the System: topic-80546.html

.. _Debugging Processes Using the Contrail Introspect Feature: topic-101832.html

.. _Monitor > Infrastructure > Dashboard: topic-82962.html

.. _Monitor > Infrastructure > Control Nodes: topic-79861.html

.. _Monitor > Infrastructure > Virtual Routers: topic-82991.html

.. _Monitor > Infrastructure > Analytics Nodes: topic-83025.html

.. _Monitor > Infrastructure > Config Nodes: topic-83026.html

.. _Monitor > Networking: topic-79862.html

.. _Query > Flows: topic-79888.html

.. _Query > Logs: topic-79863.html

.. _Understanding Flow Sampling: topic-102905.html

.. _Example\:\ Debugging Connectivity Using Monitoring for Troubleshooting: topic-83238.html

.. _Debugging Ping Failures for Policy-Connected Networks: topic-91648.html

.. _Debugging BGP Peering and Route Exchange in Contrail: topic-91656.html

.. _Troubleshooting the Floating IP Address Pool in Contrail: topic-91942.html

.. _Removing Stale Virtual Machines and Virtual Machine Interfaces: topic-91975.html

.. _Troubleshooting Link-Local Services in Contrail: topic-92355.html

.. _Getting Contrail Node Status: topic-93855.html

.. _contrail-logs (Accessing Log File Messages): topic-82960.html

.. _contrail-status (Viewing Node Status): topic-83116.html

.. _contrail-version (Viewing Version Information: topic-83118.html

.. _service (Managing Services): topic-83117.html

.. _Backing Up Contrail Databases Using JSON Format: topic-120662.html

.. _Contrail Analytics Application Programming Interfaces (APIs) and User-Visible Entities (UVEs): topic-90574.html

.. _Log and Flow Information APIs: topic-90603.html

.. _Working with Neutron: topic-91277.html

.. _Support for Amazon VPC APIs on Contrail OpenStack: topic-87799.html
