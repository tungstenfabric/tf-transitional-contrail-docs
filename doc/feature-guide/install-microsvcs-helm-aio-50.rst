.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

========================================================================
Using Helm Charts to Provision All-in-One Contrail with OpenStack Ocata
========================================================================

This is the installation procedure for using Helm charts to provision an all-in-one Contrail system with OpenStack Ocata. This is not a high availability configuration.


.. note:: All-in-one systems are only used for testing or for demonstration purposes.



-  `System Specifications`_ 


-  `Installation Steps`_ 


-  `Accessing the Contrail OpenStack Helm Cluster`_ 




System Specifications
---------------------

This procedure uses Helm to provision an OpenStack Ocata Contrail all-in-one cluster without high availability.

This procedure is tested with:

- Operating system: Ubuntu 16.04.3 LTS


- Kernel: 4.4.0-87-generic


- Docker: 1.13.1-cs9


- Helm: v2.7.2


- Kubernetes: v1.8.3


- OpenStack: Ocata


This setup was tested on a system with the following specifications:

- CPU: 8


- RAM: 32 GB


- HDD: 120 GB




Installation Steps
------------------




#. Get the contrail-helm-deployer.

   From `Juniper Networks`_  , download ``contrail-helm-deployer-5.0.0-0.40.tgz`` onto your provisioning host.

   - Untar contrail-helm-deployer-5.0.0-0.40.tgz.

       ``tar -zxf contrail-helm-deployer-5.0.0-0.40.tgz -C /opt/`` 


   



#. Export required variables.
   ::

    export BASE_DIR=$(pwd)
    export OSH_PATH=${BASE_DIR}/openstack-helm
    export OSH_INFRA_PATH=${BASE_DIR}/openstack-helm-infra
    export CHD_PATH=${BASE_DIR}/contrail-helm-deployerExport variables 



#. Install necessary packages and deploy Kubernetes.


   .. note:: If you want to install a different version of Kubernetes, CNI, or Calico, edit ``${OSH_INFRA_PATH}/tools/gate/devel/local-vars.yaml`` to override the default values in ``${OSH_INFRA_PATH}/tools/gate/playbooks/vars.yaml`` .


   ::

    cd ${OSH_PATH}
    ./tools/deployment/developer/common/001-install-packages-opencontrail.sh
    ./tools/deployment/developer/common/010-deploy-k8s.sh



#. Install OpenStack and the Heat client.
   ::

    ./tools/deployment/developer/common/020-setup-client.sh




#. Deploy OpenStack Helm-related charts.
   ::

    ./tools/deployment/developer/nfs/031-ingress-opencontrail.sh
    ./tools/deployment/developer/nfs/040-nfs-provisioner.sh
    ./tools/deployment/developer/nfs/050-mariadb.sh
    ./tools/deployment/developer/nfs/060-rabbitmq.sh
    ./tools/deployment/developer/nfs/070-memcached.sh
    ./tools/deployment/developer/nfs/080-keystone.sh
    ./tools/deployment/developer/nfs/100-horizon.sh
    ./tools/deployment/developer/nfs/120-glance.sh
    ./tools/deployment/developer/nfs/151-libvirt-opencontrail.sh
    ./tools/deployment/developer/nfs/161-compute-kit-opencontrail.sh



#. Deploy Contrail Helm charts.
   ::

    cd $CHD_PATH

    make

    # Set the IP of your CONTROL_NODES (specify your control data ip, if you have one)
    export CONTROL_NODES=10.87.65.245
    # set the control data network cidr list separated by comma and set the respective gateway
    export CONTROL_DATA_NET_LIST=10.87.65.128/25
    export VROUTER_GATEWAY=10.87.65.129

    kubectl label node opencontrail.org/controller=enabled --all
    kubectl label node opencontrail.org/vrouter-kernel=enabled --all

    kubectl replace -f ${CHD_PATH}/rbac/cluster-admin.yaml

    tee /tmp/contrail.yaml << EOF
    global:
      contrail_env:
        CONTROLLER_NODES: 172.17.0.1
        CONTROL_NODES: ${CONTROL_NODES}
        LOG_LEVEL: SYS_NOTICE
        CLOUD_ORCHESTRATOR: openstack
        AAA_MODE: cloud-admin
        CONTROL_DATA_NET_LIST: ${CONTROL_DATA_NET_LIST}
        VROUTER_GATEWAY: ${VROUTER_GATEWAY}
    EOF

    helm install --name contrail ${CHD_PATH}/contrail \
    --namespace=contrail --values=/tmp/contrail.yaml



#. Deploy Heat charts.
   ::

    cd ${OSH_PATH}
    ./tools/deployment/developer/nfs/091-heat-opencontrail.sh




Accessing the Contrail OpenStack Helm Cluster
---------------------------------------------

Use the following topic to access the OpenStack and Contrail Web UI and prepare the OpenStack client for command-line interface (CLI):

`Accessing a Contrail OpenStack Helm Cluster`_ 

**Related Documentation**

-  `Installing and Managing Contrail 5.0 Microservices Architecture Using Helm Charts`_ 

-  `Using Helm Charts to Provision Multinode Contrail OpenStack Ocata with High Availability`_ 

-  `Accessing a Contrail OpenStack Helm Cluster`_ 

-  `Frequently Asked Questions About Contrail and Helm Charts`_ 

.. _Accessing a Contrail OpenStack Helm Cluster: access_os_helm_cluster.html

.. _Installing and Managing Contrail 5.0 Microservices Architecture Using Helm Charts: install-microsvcs-helm-chart-50.html

.. _Using Helm Charts to Provision Multinode Contrail OpenStack Ocata with High Availability: install-microsvcs-helm-multi-50.html

.. _Accessing a Contrail OpenStack Helm Cluster: access_os_helm_cluster.html

.. _Frequently Asked Questions About Contrail and Helm Charts: install-microsvcs-helm-multi-faq-50.html


.. _Juniper Networks: https://www.juniper.net/support/downloads/?p=contrail#sw
