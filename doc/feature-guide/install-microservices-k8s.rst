.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===================================================
Contrail Microservices Installation with Kubernetes
===================================================

This topic provides steps for installing Contrail with microservices architecture with Kubernetes.

   -  `Installation Procedure`_ 




Installation Procedure
----------------------




#. Reimage the node to CentOS 7.4.
   ::

    /cs-shared/server-manager/client/server-manager reimage --server_id <Server ID> centos-7.4




#. Install needed tools.
   ::

    yum -y install epel-release git ansible net-tools



#. Clone the contrail-ansible-deployer repository.
   ::

    git clone https://github.com/Juniper/contrail-ansible-deployer.git
    cd contrail-ansible-deployer



#. Edit the ``config/instances.yaml`` with values appropriate for your system. The following is a sample file for a two-node Kubernetes installation.
   ::

    Sample config/instances.yaml

    provider_config:
      bms:
       ssh_pwd: <Password>
       ssh_user: root
       ssh_public_key: /root/.ssh/id_rsa.pub
       ssh_private_key: /root/.ssh/id_rsa
       domainsuffix: local
    instances:
      bms1:
       provider: bms
       roles:            # Optional.  If roles is not defined, all below roles will be created
          config_database:         # Optional.
          config:                  # Optional.
          control:                 # Optional.
          analytics_database:      # Optional.
          analytics:               # Optional.
          webui:                   # Optional.
          k8s_master:              # Optional.
          kubemanager:             # Optional.
       ip: <BMS1 IP>
      bms2:
       provider: bms
       roles:            # Optional.  If roles is not defined, all below roles will be created
         vrouter:        # Optional.
         k8s_node:       # Optional.
       ip: <BMS2 IP>
    contrail_configuration:
      CONTAINER_REGISTRY: opencontrailnightly
      CONTRAIL_VERSION: latest
      KUBERNETES_CLUSTER_PROJECT: {}



#. Turn off swap.
   ::

    swapoff -a



#. Run configure.
   ::

    ansible-playbook -i inventory/ playbooks/configure_instances.yml



#. Run install.
   ::

    ansible-playbook -i inventory/ playbooks/configure_instances.yml


**Related Documentation**

-  `Introduction to Contrail Microservices Architecture`_ 

-  `Overview of contrail-ansible-deployer for Installing Contrail with Microservices Architecture`_ 

-  `Installing Contrail with OpenStack Ocata and Kolla Ansible`_ 

.. _Introduction to Contrail Microservices Architecture: intro-microservices.html

.. _Overview of contrail-ansible-deployer for Installing Contrail with Microservices Architecture: install-contrail-overview-ansible-50.html

.. _Installing Contrail with OpenStack Ocata and Kolla Ansible: install-contrail-ocata-kolla-50.html

