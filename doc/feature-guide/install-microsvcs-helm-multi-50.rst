.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

=========================================================================================
Using Helm Charts to Provision Multinode Contrail OpenStack Ocata with High Availability
=========================================================================================

This is the installation procedure for using Helm charts to provision a multinode Contrail system with OpenStack Ocata and high availability.

-  `System Specifications`_ 


-  `Preparing to Install`_ 


-  `Installation of OpenStack Helm Charts`_ 


-  `Installation of Contrail Helm Charts`_ 


-  `Basic Testing OpenStack Helm Contrail Cluster`_ 


-  `Accessing the Contrail OpenStack Helm Cluster`_ 




System Specifications
---------------------

This procedure uses Juniper OpenStack Helm infrastructure and the OpenStack Helm repository to provision an OpenStack Ocata Contrail multinode deployment.

This procedure is tested with:

- Operating system: Ubuntu 16.04.3 LTS


- Kernel: 4.4.0-87-generic


- Docker: 1.13.1-cs9


- Helm: v2.7.2


- Kubernetes: v1.8.3


- OpenStack: Ocata




Preparing to Install
--------------------

This section is the prerequisites needed to prepare your system before provisioning multinode Contrail with OpenStack Ocata and high availability.


#. Generate SSH key on master node and copy to all nodes, in below example three nodes with IP addresses 10.13.82.43, 10.13.82.44, and 10.13.82.45 are used.
   ::

    (k8s-master)> ssh-keygen
    (k8s-master)> ssh-copy-id -i ~/.ssh/id_rsa.pub 10.13.82.43
    (k8s-master)> ssh-copy-id -i ~/.ssh/id_rsa.pub 10.13.82.44
    (k8s-master)> ssh-copy-id -i ~/.ssh/id_rsa.pub 10.13.82.45



#. Make sure NTP is configured in all nodes and each node is synched to the time-server in your environment. In below example the NTP server IP is "10.84.5.100".
   ::

     (k8s-all-nodes)> ntpq -p
     remote           refid      st t when poll reach   delay   offset  jitter
     ==============================================================================
     *10.84.5.100     66.129.255.62    2 u   15   64  377   72.421  -22.686   2.628



#. Get the contrail-helm-deployer.

    From `Juniper Networks`_  , download ``contrail-helm-deployer-5.0.0-0.40.tgz`` onto your provisioning host.

    --values ``scp contrail-helm-deployer-5.0.0-0.40.tgz`` to all nodes on your cluster.


    --valuesUntar contrail-helm-deployer-5.0.0-0.40.tgz on all nodes.

       ``tar -zxf contrail-helm-deployer-5.0.0-0.40.tgz -C /opt/`` 


   



#. Export required variables.
   ::

    (k8s-master)> cd /opt
    (k8s-master)> export BASE_DIR=$(pwd)
    (k8s-master)> export OSH_PATH=${BASE_DIR}/openstack-helm
    (k8s-master)> export OSH_INFRA_PATH=${BASE_DIR}/openstack-helm-infra
    (k8s-master)> export CHD_PATH=${BASE_DIR}/contrail-helm-deployer



#. Install necessary packages and deploy Kubernetes.


   .. note:: If you want to install a different version of Kubernetes, CNI, or Calico, edit ``${OSH_INFRA_PATH}/tools/gate/devel/local-vars.yaml`` to override the default values in ``${OSH_INFRA_PATH}/tools/gate/playbooks/vars.yaml`` .


   ::

    (k8s-master)> cd ${OSH_PATH}
    (k8s-master)> ./tools/deployment/developer/common/001-install-packages-opencontrail.sh



#. Create an inventory file on the master node for Ansible base provisioning. In the following output, 10.13.82.43/.44/.45 are the IP addresses of the nodes, and will use the SSK-key generated in Step 1.
   ::

    #!/bin/bash
    (k8s-master)> set -xe
    (k8s-master)> cat > /opt/openstack-helm-infra/tools/gate/devel/multinode-inventory.yaml <<EOF
    all:
     children:
       primary:
         hosts:
           node_one:
             ansible_port: 22
             ansible_host: 10.13.82.43
             ansible_user: root
             ansible_ssh_private_key_file: /root/.ssh/id_rsa
             ansible_ssh_extra_args: -o StrictHostKeyChecking=no
       nodes:
         hosts:
           node_two:
             ansible_port: 22
             ansible_host: 10.13.82.44
             ansible_user: root
             ansible_ssh_private_key_file: /root/.ssh/id_rsa
             ansible_ssh_extra_args: -o StrictHostKeyChecking=no
           node_three:
             ansible_port: 22
             ansible_host: 10.13.82.45
             ansible_user: root
             ansible_ssh_private_key_file: /root/.ssh/id_rsa
             ansible_ssh_extra_args: -o StrictHostKeyChecking=no
     EOF



#. Create an environment file on the master node for the cluster.


   .. note:: By default. Kubernetes v1.9.3, Helm v2.7.2, and CNI v0.6.0 are installed. If you want to install a different version. editthe ``${OSH_INFRA_PATH}/tools/gate/devel/multinode-vars.yaml`` file to override the values given in ``${OSH_INFRA_PATH}/playbooks/vars.yaml`` .



   Sample ``multinode-vars.yaml :`` 
    ::

     (k8s-master)> cat > /opt/openstack-helm-infra/tools/gate/devel/multinode-vars.yaml <<EOF
     # version fields
     version:
      kubernetes: v1.9.3
      helm: v2.7.2
      cni: v0.6.0

     kubernetes:
      network:
        # enp0s8 is your control/data interface, to which kubernetes will bind to
        default_device: enp0s8
      cluster:
        cni: calico
        pod_subnet: 192.168.0.0/16
        domain: cluster.local
     docker:
      # list of insecure_registries, from where you will be pulling container images
      insecure_registries:
        - "10.87.65.243:5000"
      # list of private secure docker registry auth info, from where you will be pulling container images
      #private_registries:
      #  - name: <docker-registry-name>
      #    username: username@abc.xyz
      #    email: username@abc.xyz
      #    password: password
      #    secret_name: contrail-image-secret
      #    namespace: openstack
     EOF



#. Run playbooks on the master node.
   ::

    (k8s-master)> set -xe
    (k8s-master)> cd ${OSH_INFRA_PATH}
    (k8s-master)> make dev-deploy setup-host multinode
    (k8s-master)> make dev-deploy k8s multinode




#. Verify the ``kube-dns`` connection from all nodes. Use ``nslookup`` to verify that you are able to resolve Kubernetes cluster-specific names.
   ::

     (k8s-all-nodes)> nslookup
     > kubernetes.default.svc.cluster.local
     Server:         10.96.0.10
     Address:        10.96.0.10#53

     Non-authoritative answer:
     Name:   kubernetes.default.svc.cluster.local
     Address: 10.96.0.1




Installation of OpenStack Helm Charts
-------------------------------------

Use this procedure to install the OpenStack Helm charts.


#. Before installing the OpenStack Helm charts, review the default labels for the nodes.

   The default nodes have the labels ``openstack-control-plane`` and ``openstack-compute-node`` .The default configuration creates OpenStack Helm (OSH) pods on all the nodes. Use the following commands to check the default OpenStack labels.
   ::

    (k8s-master)>  kubectl get nodes -o wide -l openstack-control-plane=enabled
    (k8s-master)> kubectl get nodes -o wide -l openstack-compute-node=enabled

   If you need to restrict the creation of OSH pods on specific nodes, disable the OpenStack labels. The following example shows how to disable the ``openstack-compute-node`` label on the ``ubuntu-contrail-9`` node.
   ::

    (k8s-master)> kubectl label node ubuntu-contrail-9 --overwrite openstack-compute-node=disabled




#. Deploy OpenStack Helm charts.
   ::

    (k8s-master)> set -xe
    (k8s-master)> cd ${OSH_PATH}

    (k8s-master)> ./tools/deployment/multinode/010-setup-client.sh
    (k8s-master)> ./tools/deployment/multinode/021-ingress-opencontrail.sh
    (k8s-master)> ./tools/deployment/multinode/030-ceph.sh
    (k8s-master)> ./tools/deployment/multinode/040-ceph-ns-activate.sh
    (k8s-master)> ./tools/deployment/multinode/050-mariadb.sh
    (k8s-master)> ./tools/deployment/multinode/060-rabbitmq.sh
    (k8s-master)> ./tools/deployment/multinode/070-memcached.sh
    (k8s-master)> ./tools/deployment/multinode/080-keystone.sh
    (k8s-master)> ./tools/deployment/multinode/090-ceph-radosgateway.sh
    (k8s-master)> ./tools/deployment/multinode/100-glance.sh
    (k8s-master)> ./tools/deployment/multinode/110-cinder.sh
    (k8s-master)> ./tools/deployment/multinode/131-libvirt-opencontrail.sh
    # Edit ${OSH_PATH}/tools/overrides/backends/opencontrail/nova.yaml and
    # ${OSH_PATH}/tools/overrides/backends/opencontrail/neutron.yaml
    # to make sure that you are pulling init container image from correct registry and tag
    (k8s-master)> ./tools/deployment/multinode/141-compute-kit-opencontrail.sh
    (k8s-master)> ./tools/deployment/developer/ceph/100-horizon.sh




Installation of Contrail Helm Charts
------------------------------------

Use this procedure to install the Contrail Helm charts.


#. Label the Contrail pods. All Contrail pods are to be deployed in the namespace ``contrail`` , using the following labels:

   - Control nodes—opencontrail.org/controller


   - vRouter kernel—opencontrail.org/vrouter-kernel


   - vRouter DPDK—opencontrail.org/vrouter-dpdk


   The following example shows how to label ``ubuntu-contrail-11`` as DPDK and label ``ubuntu-contrail-10`` as kernel vrouter.
    ::

    (k8s-master)> kubectl label node  ubuntu-contrail-11 opencontrail.org/vrouter-dpdk=enabled
    (k8s-master)> kubectl label node ubuntu-contrail-10 opencontrail.org/vrouter-kernel=enabled
    (k8s-master)> kubectl label nodes ubuntu-contrail-9 ubuntu-contrail-10 ubuntu-contrail-11 opencontrail.org/controller=enabled



#. Create Kubernetes ClusterRoleBinding for Contrail.
   ::

    (k8s-master)> cd $CHD_PATH
    (k8s-master)> kubectl replace -f ${CHD_PATH}/rbac/cluster-admin.yaml



#. Set up the Contrail Helm charts and set the configuration settings specific to your system in the values.yaml file for each of the charts.

   ::

    (k8s-master)> cd $CHD_PATH
    (k8s-master)> make

    # Please note in below example, 192.168.1.0/24 is "Control/Data" network
    # Export variables
    (k8s-master)> export CONTROLLER_NODES="192.168.1.43,192.168.1.44,192.168.1.45"
    (k8s-master)> export VROUTER_GATEWAY="192.168.1.1"
    (k8s-master)> export CONTROL_DATA_NET_LIST="192.168.1.0/24"
    (k8s-master)> export BGP_PORT="1179"

    # [Optional] By default, it will pull latest image from opencontrailnightly

    (k8s-master)> export CONTRAIL_REGISTRY="opencontrailnightly"
    (k8s-master)> export CONTRAIL_TAG="latest"

    # [Optional] only if you are pulling images from a private docker registry
    export CONTRAIL_REG_USERNAME="abc@abc.com"
    export CONTRAIL_REG_PASSWORD="password"

    tee /tmp/contrail-env-images.yaml << EOF
    global:
      contrail_env:
        CONTROLLER_NODES: ${CONTROLLER_NODES}
        CONTROL_NODES: ${CONTROL_NODES:-CONTROLLER_NODES}
        LOG_LEVEL: SYS_NOTICE
        CLOUD_ORCHESTRATOR: openstack
        AAA_MODE: cloud-admin
        VROUTER_GATEWAY: ${VROUTER_GATEWAY}
        BGP_PORT: ${BGP_PORT}
      contrail_env_vrouter_kernel:
        CONTROL_DATA_NET_LIST: ${CONTROL_DATA_NET_LIST}
        AGENT_MODE: nic
      contrail_env_vrouter_dpdk:
        AGENT_MODE: dpdk
      images:
        tags:
          kafka: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-external-kafka:${CONTRAIL_TAG:-latest}"
          cassandra: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-external-cassandra:${CONTRAIL_TAG:-latest}"
          redis: "redis:4.0.2"
          zookeeper: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-external-zookeeper:${CONTRAIL_TAG:-latest}"
          contrail_control: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-controller-control-control:${CONTRAIL_TAG:-latest}"
          control_dns: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-controller-control-dns:${CONTRAIL_TAG:-latest}"
          control_named: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-controller-control-named:${CONTRAIL_TAG:-latest}"
          config_api: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-controller-config-api:${CONTRAIL_TAG:-latest}"
          config_devicemgr: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-controller-config-devicemgr:${CONTRAIL_TAG:-latest}"
          config_schema_transformer: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-controller-config-schema:${CONTRAIL_TAG:-latest}"
          config_svcmonitor: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-controller-config-svcmonitor:${CONTRAIL_TAG:-latest}"
          webui_middleware: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-controller-webui-job:${CONTRAIL_TAG:-latest}"
          webui: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-controller-webui-web:${CONTRAIL_TAG:-latest}"
          analytics_api: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-analytics-api:${CONTRAIL_TAG:-latest}"
          contrail_collector: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-analytics-collector:${CONTRAIL_TAG:-latest}"
          analytics_alarm_gen: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-analytics-alarm-gen:${CONTRAIL_TAG:-latest}"
          analytics_query_engine: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-analytics-query-engine:${CONTRAIL_TAG:-latest}"
          analytics_snmp_collector: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-analytics-snmp-collector:${CONTRAIL_TAG:-latest}"
          contrail_topology: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-analytics-topology:${CONTRAIL_TAG:-latest}"
          build_driver_init: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-vrouter-kernel-build-init:${CONTRAIL_TAG:-latest}"
          vrouter_agent: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-vrouter-agent:${CONTRAIL_TAG:-latest}"
          vrouter_init_kernel: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-vrouter-kernel-init:${CONTRAIL_TAG:-latest}"
          vrouter_dpdk: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-vrouter-agent-dpdk:${CONTRAIL_TAG:-latest}"
          vrouter_init_dpdk: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-vrouter-kernel-init-dpdk:${CONTRAIL_TAG:-latest}"
          nodemgr: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-nodemgr:${CONTRAIL_TAG:-latest}"
          contrail_status: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-status:${CONTRAIL_TAG:-latest}"
          node_init: "${CONTRAIL_REGISTRY:-opencontrailnightly}/contrail-node-init:${CONTRAIL_TAG:-latest}"
          dep_check: quay.io/stackanetes/kubernetes-entrypoint:v0.2.1
    EOF


   .. note:: If any other environment variables need to be added, add them in the values.yaml file of the respective charts.


   ::

    # [Optional] only if you are pulling contrail images from a private registry
    tee /tmp/contrail-registry-auth.yaml << EOF
    global:
     images:
       imageCredentials:
         registry: ${CONTRAIL_REGISTRY:-opencontrailnightly}
         username: ${CONTRAIL_REG_USERNAME}
         password: ${CONTRAIL_REG_PASSWORD}
    EOF

    # [Optional] only if you are pulling images from a private registry export CONTRAIL_REGISTRY_ARG="--values=/tmp/contrail-registry-auth.yaml "



#. Use Helm install commands to deploy each of the Contrail Helm charts.
   ::

     (k8s-master)> helm install --name contrail-thirdparty ${CHD_PATH}/contrail-thirdparty \
     --namespace=contrail \
     --values=/tmp/contrail-env-images.yaml \
     ${CONTRAIL_REGISTRY_ARG}

     (k8s-master)> helm install --name contrail-controller ${CHD_PATH}/contrail-controller \
     --namespace=contrail \
     --values=/tmp/contrail-env-images.yaml \
     ${CONTRAIL_REGISTRY_ARG}

     (k8s-master)> helm install --name contrail-analytics ${CHD_PATH}/contrail-analytics \
     --namespace=contrail \
     --values=/tmp/contrail-env-images.yaml \
     ${CONTRAIL_REGISTRY_ARG}

     # Edit contrail-vrouter/values.yaml and make sure that global.images.tags.vrouter_init_kernel is right. Image tag name will be different depending upon your linux. Also set the global.node.host_os to ubuntu or centos depending on your system

     (k8s-master)> helm install --name contrail-vrouter ${CHD_PATH}/contrail-vrouter \
     --namespace=contrail \
     --values=/tmp/contrail-env-images.yaml \
     ${CONTRAIL_REGISTRY_ARG}



#. When the Contrail pods are up and running, deploy the OpenStack Heat chart.
   ::

    # Edit ${OSH_PATH}/tools/overrides/backends/opencontrail/nova.yaml and
    # ${OSH_PATH}/tools/overrides/backends/opencontrail/heat.yaml  
    # to make sure that you are pulling the right opencontrail init container image
    (k8s-master)> ./tools/deployment/multinode/151-heat-opencontrail.sh



#. When finished, run the compute kit test.

    ``(k8s-master)> ./tools/deployment/multinode/143-compute-kit-opencontrail-test.sh`` 




Basic Testing OpenStack Helm Contrail Cluster
---------------------------------------------

Use the following commands to perform basic testing on the virtual network and the virtual machines in your OpenStack Helm Contrail cluster.
::

 (k8s-master)> export OS_CLOUD=openstack_helm

 (k8s-master)> openstack network create MGMT-VN
 (k8s-master)> openstack subnet create --subnet-range 172.16.1.0/24 --network MGMT-VN MGMT-VN-subnet

 (k8s-master)> openstack server create --flavor m1.tiny --image 'Cirros 0.3.5 64-bit' \
 --nic net-id=MGMT-VN \
 Test-01

 (k8s-master)> openstack server create --flavor m1.tiny --image 'Cirros 0.3.5 64-bit' \
 --nic net-id=MGMT-VN \
 Test-02



Accessing the Contrail OpenStack Helm Cluster
---------------------------------------------

Use the following topic to access the OpenStack and Contrail Web UI and prepare the OpenStack client for command-line interface (CLI):

`Accessing a Contrail OpenStack Helm Cluster`_ 

**Related Documentation**

-  `Installing and Managing Contrail 5.0 Microservices Architecture Using Helm Charts`_ 

-  `Frequently Asked Questions About Contrail and Helm Charts`_ 

-  `Using Helm Charts to Provision All-in-One Contrail with OpenStack Ocata`_ 

-  `Accessing a Contrail OpenStack Helm Cluster`_ 

.. _Accessing a Contrail OpenStack Helm Cluster: access_os_helm_cluster.html

.. _Installing and Managing Contrail 5.0 Microservices Architecture Using Helm Charts: install-microsvcs-helm-chart-50.html

.. _Frequently Asked Questions About Contrail and Helm Charts: install-microsvcs-helm-multi-faq-50.html

.. _Using Helm Charts to Provision All-in-One Contrail with OpenStack Ocata: install-microsvcs-helm-aio-50.html

.. _Accessing a Contrail OpenStack Helm Cluster: access_os_helm_cluster.html


.. _Juniper Networks: https://www.juniper.net/support/downloads/?p=contrail#sw
