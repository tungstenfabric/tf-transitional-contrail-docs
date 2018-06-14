.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

=================================================================================
Installing and Managing Contrail 5.0 Microservices Architecture Using Helm Charts
=================================================================================

Contrail 5.0 introduces microservices architecture. This section provides an overview of using Helm charts in preparation for installing Contrail Networking with a microservices architecture. For an introduction to Contrail microservices, refer to `Introduction to Contrail Microservices Architecture`_ .

-  `Understanding Helm Charts`_ 


-  `Features of Contrail Helm Deployer`_ 


-  `Contrail Kubernetes Resource implementation`_ 


-  `Defining Contrail Pods on Kubernetes`_ 


-  `Installing Contrail Using Helm Charts`_ 




Understanding Helm Charts
-------------------------

Helm is the package manager for Kubernetes, an open source software for managing containerized systems. The packaging format used by Helm is a chart, a collection of files that describe a related set of Kubernetes resources. Helm charts enable you to define, install, and configure your Kubernetes application. A chart can be used to deploy something simple, like a memcached pod, or something complex, like a full web application stack complete with HTTP servers, databases, and the like.

Starting with Contrail 5.0, Contrail Helm charts give you complete life cycle management of installation, update, and delete of Contrail Docker-based containers in a microservices architecture.



Features of Contrail Helm Deployer
----------------------------------

The Contrail Helm deployer supports deploying Contrail for the following orchestrators:

- OpenStack


- Kubernetes




Contrail Helm Deployer Charts
------------------------------

The Contrail Helm deployer uses the following charts.

-  **helm-toolkit chart** 

Contains common templates and functions that are used by every other Contrail Helm chart.


-  **contrail-thirdparty chart** 

Defines and deploys third party containers as Kubernetes resources for Contrail, including:

- RabbitMQ


- ZooKeeper


- Cassandra


- Kafka


- Redis



-  **contrail-controller chart** 

Deploys and manages Contrail components as Kubernetes resources, including:

- control


- config


- webui



-  **contrail-analytics chart** 

Deploys and manages Contrail analytics components as Kubernetes resources.


-  **contrail-vrouter chart** 

Deploys and manages Contrail vrouter components as Kubernetes resources.


-  **contrail-superset chart** 

A superset of all other Contrail Helm charts, can be used to install all Kubernetes resources defined in other Contrail charts.




Contrail Kubernetes Resource implementation
-------------------------------------------

All Contrail Helm charts follow a similar approach to implementing Kubernetes resources. For each of the Contrail 5.0 containers, configuration input is given as an environment variable in the file ``values.yaml`` . Use the variable ``.Values.contrail_env`` to define environment variables for the containers.
::

  contrail_env:
  CONTROLLER_NODES: 10.87.65.248
  LOG_LEVEL: SYS_NOTICE
  CLOUD_ORCHESTRATOR: openstack
  AAA_MODE: cloud-admin

All of the environment variables are stored in Kubernetes resources called configmaps. The configmaps are loaded into specific containers as environment variables.

Because Contrail is an infrastructure-level application, every pod of Contrail is hosted on the host network namespace. Consequently, the daemonset controller is used to define all Contrail pods, so that each of the Contrail pods are brought up on different nodes to avoid port conflicts.



Defining Contrail Pods on Kubernetes
------------------------------------

The Contrail helm deployer provides the options to logically group containers into pods or to deploy each container as a different pod. If ``.Values.manifests.each_container_is_pod`` is set to ``true`` , then each container is deployed as a pod.If the value is set to ``false`` , the containers are logically grouped into a pod.



Example: Contrail Pods Deployment Options
-----------------------------------------

In the following example, if ``.Values.manifests.each_container_is_pod`` is ``true`` , each container will be deployed as a pod.

If ``.Values.manifests.each_container_is_pod`` is ``false`` , the containers are logically grouped into pods.


.. note:: By default, the ``contrail-thirdparty`` Helm chart creates a separate pod for each of the third party services.


::

    pods:
    - contrail-control
      containers:
        - contrail-control
        - contrail-dns
        - contrail-named
        - control-nodemgr
    - contrail-config
      containers:
        - config-api
        - schema-transformer
        - svc-monitor
        - device-manager
        - config-nodemgr
    - contrail-webui
      containers:
        - contrail-webui
        - contrail-middleware
    - contrail-analytics
      containers:
        - analytics-api
        - analytics-colletor
        - snmp-collector
        - query-engine
        - alarm-gen
        - contrail-topology
    - contrail-vrouter
      containers:
        - vrouter-kernel/vrouter-dpdk/vrouter-sriov
        - vrouter-agent
        - vrouter-nodemgr



Installing Contrail Using Helm Charts
-------------------------------------

Use one of the following procedures to install Contrail with OpenStack Ocata using Helm charts:

-  `Using Helm Charts to Provision Multinode Contrail OpenStack Ocata with High Availability`_ 


-  `Using Helm Charts to Provision All-in-One Contrail with OpenStack Ocata`_ 


**Related Documentation**

-  `Using Helm Charts to Provision Multinode Contrail OpenStack Ocata with High Availability`_ 

-  `Using Helm Charts to Provision All-in-One Contrail with OpenStack Ocata`_ 

-  `Accessing a Contrail OpenStack Helm Cluster`_ 

-  `Frequently Asked Questions About Contrail and Helm Charts`_ 

.. _Introduction to Contrail Microservices Architecture: intro-microservices.html

.. _Using Helm Charts to Provision Multinode Contrail OpenStack Ocata with High Availability: install-microsvcs-helm-multi-50.html

.. _Using Helm Charts to Provision All-in-One Contrail with OpenStack Ocata: install-microsvcs-helm-aio-50.html

.. _Using Helm Charts to Provision Multinode Contrail OpenStack Ocata with High Availability: install-microsvcs-helm-multi-50.html

.. _Using Helm Charts to Provision All-in-One Contrail with OpenStack Ocata: install-microsvcs-helm-aio-50.html

.. _Accessing a Contrail OpenStack Helm Cluster: access_os_helm_cluster.html

.. _Frequently Asked Questions About Contrail and Helm Charts: install-microsvcs-helm-multi-faq-50.html

