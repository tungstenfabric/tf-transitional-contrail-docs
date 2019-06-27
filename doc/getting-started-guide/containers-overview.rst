.. This work is licensed under the Creative Commons Attribution 4.0 International License.
.. To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

=====================================================
Introduction to Containerized Tungsten Fabric Modules
=====================================================

Starting with Release 4.0, some subsystems of Tungsten Fabric are delivered as Docker containers.



-  `Why Use Containers?`_ 


-  `Overview of Tungsten Fabric Containers`_ 


-  `Release 4.0 Containers`_ 


-  `DPDK vRouter`_ 


-  `Summary of Container Design, Configuration Management, and Orchestration`_ 




Why Use Containers?
-------------------

Tungsten Fabric software releases are distributed as sets of packages for each of the subsystem modules of a Tungsten Fabric system. The Tungsten Fabric modules depend on numerous open source packages and provisioning tools and are validated on specific Linux distributions. Each module has its own dependency chains and its own configuration parameters.

These dependencies lead to complexities of deployment, including:

- The Linux version of the target system must match exactly to the version upon which Tungsten Fabric is qualified, or the installation might fail.


- A deployment that succeeds despite an operating system mismatch could pull dependent packages from a customer mirror site that don’t match the dependencies with which the Tungsten Fabric system was qualified, creating potential for failure.


- Change in any package on the target system creates a risk of failure of dependencies in the Tungsten Fabric software, creating a need for requalification upon any system change.


- Currently, provisioning tools such as Fuel, Juju, Puppet, and the like interact directly with Tungsten Fabric services. Over time, these tools become more complex, requiring interaction with the lowest level of details of Tungsten Fabric service parameters.


Containerizing some Tungsten Fabric subsystems reduces the complexity of deploying Tungsten Fabric and provides a straightforward, simple way to deploy and operate Tungsten Fabric.



Overview of Tungsten Fabric Containers
--------------------------------------

Starting with Release 4.0, some of the Tungsten Fabric subsystems are delivered as Docker containers that group together related functional components. Each container file includes an INI-based configuration file for configuring the services within the container. The purpose of the INI is to provide enough high-level configuration entries to configure all services within the container, while masking the complexity of the internal service configuration. The container configuration files are available on the host system and mounted within specific containers.

In Release 4.0, the containerized components include Tungsten Fabric controller, analytics, and load-balancer applications. Tungsten Fabric OpenStack components are not containerized at this time.

In Release 4.0.1, the containerized components include OpenStack Ocata services. Only OpenStack Ocata services are containerized. Mitaka and Newton SKUs of OpenStack are still provisioned as non-containerized host services.

All Tungsten Fabric containers run with the host network, without using a Docker bridge, however, all services within the container listen on the host network interface. Some services, such as RabbitMQ, require extra parameters, such as a host-based PID namespace.

The intention is to build a composable Tungsten Fabric core system of containers that can be used with differing cloud and container orchestration systems, such as OpenStack, Kubernetes, Mesos, and the like.

.. _Figure 1: 

.. _Figure 1\:\ Sample Configuration Containerized Tungsten Fabric:

*Figure 1* : Sample Configuration Containerized Tungsten Fabric

.. figure:: s019890.gif



Release 4.0 Containers
-----------------------

This section describes the containers in Release 4.0 and their contents.

-  `contrail-controller`_ 


-  `contrail-analytics`_ 


-  `contrail-analyticsdb`_ 


-  `contrail-lb`_ 




contrail-controller
-------------------

The ``contrail-controller`` container includes all Tungsten Fabric applications that make up a Tungsten Fabric controller, including:

- All configuration services, such as ``contrail api, config-nodemgr, device-manager, schema, svc-monitor`` , and CONFIGDB.


- All control services, such as ``contrail-control, control-nodemgr, contrail-dns`` , and ``contrail-named`` .


- All Web UI services, such as ``contrail-webui`` and ``contrail-webui-middleware`` .


- Configuration database (Cassandra)


- Zookeeper


- RabbitMQ


- Redis for Web Ui




contrail-analytics
------------------

The ``contrail-analytics`` container includes all Tungsten Fabric analytics services, including:

-  ``alarm-gen`` 


-  ``analytics-api`` 


-  ``analytics-nodemgr`` 


-  ``contrail-collector`` 


-  ``query-engine``  


-  ``snmp-collector`` 


-  ``contrail-topology`` 




contrail-analyticsdb
--------------------

The ``contrail-analyticsdb`` container has Cassandra for the analytics database and Kafka for streaming data.



contrail-lb
-----------

The ``contrail-lb`` loadbalancer container includes all components that provide load-balancing and high availability to the system, such as HAproxy, keepalive, and the like.

In previous releases of Tungsten Fabric, HAproxy and keepalive were included in most services to load-balance Tungsten Fabric service endpoints. Starting with Release 4.0, the load-balancers are taken out of the individual services and held instead in a dedicated ``loadbalancer`` container. An exception is HAproxy as part of the vrouter agent, which can be used to implement Load-Balancing as a Service (LBaaS).

The ``loadbalancer`` container is an optional container, and customers can choose to use their own load-balancing system.



DPDK vRouter
------------

Starting with Tungsten Fabric release 5.0, you can configure the Tungsten Fabric DPDK vRouter to run in a Docker container. In earlier releases, DPDK vRouter runs on a compute host. The contrail-vrouter-dpdk binary file provides data plane functionality when Tungsten Fabric vRouter is run in DPDK mode in a Tungsten Fabric cluster.



Summary of Container Design, Configuration Management, and Orchestration
------------------------------------------------------------------------

The following are key features of the new architecture of Tungsten Fabric containers.

- All of the Tungsten Fabric containers are multiprocess Docker containers.


- Each container has an INI-based configuration file that has the configurations for all of the applications running in that container.


- The user toolset contrailctl is used to manage the container configuration files.


- Each container is self-contained, with minimal external orchestration needs.


- A single tool, Ansible, is used for all levels of building, deploying, and provisioning the containers. The Ansible code for the Tungsten Fabric system is named ``contrail-ansible`` and kept in a separate repository. The Tungsten Fabric Ansible code is responsible for all aspects of Tungsten Fabric container build, deployment, and basic container orchestration.


**Related Documentation**

-  `Using contrailctl to Configure Services Within Containers`_ 

.. _Using contrailctl to Configure Services Within Containers: contrailctl.html

