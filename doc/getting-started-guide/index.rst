.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

=====================================
Tungsten Fabric Getting Started Guide
=====================================

* Overview

  * Understanding Tungsten Fabric

    * `Tungsten Fabric Overview`_

    * `Tungsten Fabric Description`_

* Installing and Upgrading Tungsten Fabric

  * Server Requirements and Supported Platforms

    * `Server Requirements and Supported Platforms`_

  * Installing Tungsten Fabric and Provisioning Roles
  
    * `Introduction to Containerized Tungsten Fabric Modules`_

    * `Downloading Installation Software`_

    * `Overview of contrail-ansible-deployer used in Contrail Command for Installing Tungsten Fabric with Microservices Architecture`_

    * `Installing Tungsten Fabric with OpenStack and Kolla Ansible`_

    * `Supporting Multiple Interfaces on Servers and Nodes`_

    * `Configuring the Control Node with BGP`_

    * `Adding a New Node to an Existing Containerized Tungsten Fabric Cluster`_

    * `Using contrailctl to Configure Services Within Containers`_

    * `Tungsten Fabric Global Controller`_

    * `Role and Resource-Based Access Control`_

  * Installation and Configuration Scenarios

    * `Setting Up and Using a Simple Virtual Gateway with Release 4.0`_

    * `Simple Underlay Connectivity without Gateway`_

    * `Dynamic Kernel Module Support (DKMS) for vRouter`_

  * Upgrading Tungsten Fabric Software

  * Contrail Command

  * Using Tungsten Fabric with Red Hat

* Configuring Tungsten Fabric

  * Configuring Virtual Networks

    * `Creating Projects in OpenStack for Configuring Tenants in Tungsten Fabric`_

    * `Creating a Virtual Network with Tungsten Fabric`_

    * `Creating a Virtual Network with OpenStack Tungsten Fabric`_

    * `Creating an Image for a Project in OpenStack Tungsten Fabric`_

    * `Creating a Floating IP Address Pool`_

    * `Using Security Groups with Virtual Machines (Instances)`_

    * `Support for IPv6 Networks in Tungsten Fabric`_

    * `Configuring EVPN and VXLAN`_

  * Example of Deploying a Multi-Tier Web Application Using Tungsten Fabric

    * `Example\:\ Deploying a Multi-Tier Web Application`_

    * `Sample Network Configuration for Devices for Simple Tiered Web Application`_

  * Configuring Services

    * `Configuring DNS Servers`_

    * `Support for Multicast`_

    * `Using Static Routes with Services`_

    * `Configuring Metadata Service`_

  * Configuring Service Chaining

    * `Service Chaining`_

    * `Service Chaining MX Series Configuration`_

    * `ECMP Load Balancing in the Service Chain`_

    * `Customized Hash Field Selection for ECMP Load Balancing`_

    * `Using the Tungsten Fabric Heat Template`_

    * `Service Chain Route Reorigination`_

    * `Service Instance Health Checks`_

  * Examples\:\ Configuring Service Chaining

* Monitoring and Troubleshooting the Network Using Tungsten Fabric Analytics

  * Understanding Tungsten Fabric Analytics

    * `Understanding Tungsten Fabric Analytics`_

    * `Tungsten Fabric Alerts`_

    * `Underlay Overlay Mapping in Tungsten Fabric`_

  * Configuring Tungsten Fabric Analytics

    * `Analytics Scalability`_

    * `High Availability for Analytics`_

    * `Role-Based Access Control for Analytics`_

    * `System Log Receiver in Tungsten Fabric Analytics`_

    * `Sending Flow Messages to the Tungsten Fabric System Log`_

    * `More Efficient Flow Queries`_

    * `Ceilometer Support in a Tungsten Fabric Cloud`_

  * Using Tungsten Fabric Analytics to Monitor and Troubleshoot the Network

    * `Monitoring the System`_

    * `Debugging Processes Using the Tungsten Fabric Introspect Feature`_

    * `Monitor > Infrastructure > Dashboard`_

    * `Monitor > Infrastructure > Control Nodes`_

    * `Monitor > Infrastructure > Virtual Routers`_

    * `Monitor > Infrastructure > Analytics Nodes`_

    * `Monitor > Infrastructure > Config Nodes`_

    * `Monitor > Networking`_

    * `Query > Flows`_

    * `Query > Logs`_

    * `Example\:\ Debugging Connectivity Using Monitoring for Troubleshooting`_

.. toctree::
   :maxdepth: 2
   :titlesonly:
   :glob:
   :hidden:

   overview-virtual-network-controller.rst
   components-vnc.rst
   hardware-reqs-vnc.rst
   download-software-vnc.rst
   install-contrail-overview-ansible-50.rst
   install-contrail-ocata-kolla-50.rst
   admin-control-node.rst
   role-resource-access-control-vmc.rst
   simple-gateway-support-vnc-40.rst
   underlay-no-gateway.rst
   dkms-support-vncxml.rst
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
   broadcast-vnc.rst
   static-routes-for-services-vnc.rst
   configure-metadata-service-vnc.rst
   service-chaining-vnc.rst
   service-chaining-mx.rst
   load-balancing-vnc.rst
   custom-field-hash-vnc.rst
   heat-template-vnc.rst
   service-chain-route-reorig-vnc.rst
   service-instance-health-check.rst
   analytics-overview-vnc.rst
   alerts-overview.rst
   underlay-overlay-mapping-vnc.rst
   analytics-scalability-vnc.rst
   ha-analytics-vnc.rst
   rbac-analytics.rst
   syslog-receiver-vnc.rst
   send-flow-msg-syslog.rst
   efficient-flow-queries.rst
   ceilometer-configuring.rst
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
   debug-connectivity-vnc.rst
   add-node-existing-container.rst
   containers-overview.rst
   contrailctl.rst
   global-controller-vnc.rst
   multi-interface-40.rst

.. _END USER LICENSE AGREEMENT: copyright.html

.. _Table of Contents: OUTPUT-BASE-FILENAME-TOC.html

.. _Tungsten Fabric Overview: overview-virtual-network-controller.html

.. _Tungsten Fabric Description: components-vnc.html

.. _Server Requirements and Supported Platforms: hardware-reqs-vnc.html

.. _Downloading Installation Software: download-software-vnc.html

.. _Overview of contrail-ansible-deployer used in Contrail Command for Installing Tungsten Fabric with Microservices Architecture: install-contrail-overview-ansible-50.html

.. _Installing Tungsten Fabric with OpenStack and Kolla Ansible: install-contrail-ocata-kolla-50.html

.. _Configuring the Control Node with BGP: admin-control-node.html

.. _Role and Resource-Based Access Control: role-resource-access-control-vmc.html

.. _Setting Up and Using a Simple Virtual Gateway with Release 4.0: simple-gateway-support-vnc-40.html

.. _Simple Underlay Connectivity without Gateway: underlay-no-gateway.html

.. _Dynamic Kernel Module Support (DKMS) for vRouter: dkms-support-vncxml.html

.. _Creating Projects in OpenStack for Configuring Tenants in Tungsten Fabric: creating-projects-vnc.html

.. _Creating a Virtual Network with Tungsten Fabric: creating-virtual-network-juniper-vnc.html

.. _Creating a Virtual Network with OpenStack Tungsten Fabric: creating-virtual-network-vnc.html

.. _Creating an Image for a Project in OpenStack Tungsten Fabric: creating-image-vnc.html

.. _Creating a Floating IP Address Pool: creating-ip-address-pool-vnc.html

.. _Using Security Groups with Virtual Machines (Instances): creating-security-groups.html

.. _Support for IPv6 Networks in Tungsten Fabric: ipv6-networks-vnc.html

.. _Configuring EVPN and VXLAN: evpn-vxlan-configuring.html

.. _Example\:\ Deploying a Multi-Tier Web Application: web-use-case-vnc.html

.. _Sample Network Configuration for Devices for Simple Tiered Web Application: code-example-vnc.html

.. _Configuring DNS Servers: configure-dns-vnc.html

.. _Support for Multicast: broadcast-vnc.html

.. _Using Static Routes with Services: static-routes-for-services-vnc.html

.. _Configuring Metadata Service: configure-metadata-service-vnc.html

.. _Service Chaining: service-chaining-vnc.html

.. _Service Chaining MX Series Configuration: service-chaining-mx.html

.. _ECMP Load Balancing in the Service Chain: load-balancing-vnc.html

.. _Customized Hash Field Selection for ECMP Load Balancing: custom-field-hash-vnc.html

.. _Using the Tungsten Fabric Heat Template: heat-template-vnc.html

.. _Service Chain Route Reorigination: service-chain-route-reorig-vnc.html

.. _Service Instance Health Checks: service-instance-health-check.html

.. _Understanding Tungsten Fabric Analytics: analytics-overview-vnc.html

.. _Tungsten Fabric Alerts: alerts-overview.html

.. _Underlay Overlay Mapping in Tungsten Fabric: underlay-overlay-mapping-vnc.html

.. _Analytics Scalability: analytics-scalability-vnc.html

.. _High Availability for Analytics: ha-analytics-vnc.html

.. _Role-Based Access Control for Analytics: rbac-analytics.html

.. _System Log Receiver in Tungsten Fabric Analytics: syslog-receiver-vnc.html

.. _Sending Flow Messages to the Tungsten Fabric System Log: send-flow-msg-syslog.html

.. _More Efficient Flow Queries: efficient-flow-queries.html

.. _Ceilometer Support in a Tungsten Fabric Cloud: ceilometer-configuring.html

.. _Monitoring the System: monitor-vnc.html

.. _Debugging Processes Using the Tungsten Fabric Introspect Feature: introspect-process-debugging.html

.. _Monitor > Infrastructure > Dashboard: monitor-dashboard-vnc.html

.. _Monitor > Infrastructure > Control Nodes: monitoring-infrastructure-vnc.html

.. _Monitor > Infrastructure > Virtual Routers: monitoring-vrouters-vnc.html

.. _Monitor > Infrastructure > Analytics Nodes: monitor-analytics-vnc.html

.. _Monitor > Infrastructure > Config Nodes: monitor-config-vnc.html

.. _Monitor > Networking: monitoring-networking-vnc.html

.. _Query > Flows: monitoring-flow-vnc.html

.. _Query > Logs: monitoring-syslog-vnc.html

.. _Example\:\ Debugging Connectivity Using Monitoring for Troubleshooting: debug-connectivity-vnc.html

.. _Adding a New Node to an Existing Containerized Tungsten Fabric Cluster: add-node-existing-container.html

.. _Introduction to Containerized Tungsten Fabric Modules: containers-overview.html

.. _Using contrailctl to Configure Services Within Containers: contrailctl.html

.. _Tungsten Fabric Global Controller: global-controller-vnc.html

.. _Supporting Multiple Interfaces on Servers and Nodes:   multi-interface-40.html
