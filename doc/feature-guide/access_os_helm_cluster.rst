.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

===========================================
Accessing a Contrail OpenStack Helm Cluster
===========================================

When the provisioning of Contrail with Helm charts is completed, use this topic to access the OpenStack and Contrail Web UI and prepare the OpenStack client for command-line interface (CLI).

-  `Overview`_ 


-  `Installing the OpenStack Client`_ 


-  `Create openstackrc File and Test OpenStack Client`_ 


-  `Accessing the Contrail Web UI`_ 


-  `Accessing OpenStack Horizon`_ 


-  `Accessing the Virtual Machine Console from Horizon`_ 


-  `OpenStack References`_ 




Overview
--------

This topic assumes you have already installed Contrail and OpenStack using Helm charts, typically by using these procedures:

-  `Installing and Managing Contrail 5.0 Microservices Architecture Using Helm Charts`_ 


-  `Using Helm Charts to Provision Multinode Contrail OpenStack Ocata with High Availability`_ 


-  `Using Helm Charts to Provision All-in-One Contrail with OpenStack Ocata`_ 


-  `Frequently Asked Questions About Contrail and Helm Charts`_ 






Installing the OpenStack Client
-------------------------------

Use this procedure to install the OpenStack CLI tool.


#. Install the OpenStack client CLI tool on the master Ubuntu host.
   ::

    apt install python-dev python-pip -y
    pip install --upgrade pip
    pip install python-openstackclient    OR
    apt-get install python-openstackclient



#. If you have problems installing the python-dev package, add another repository.
   ::

    Add following repo to source "/etc/apt/sources.list"
    deb http://archive.ubuntu.com/ubuntu/ xenial-updates main universe multiverse
    apt-get update
    apt-get install python-dev




Create openstackrc File and Test OpenStack Client
--------------------------------------------------


#. Create an openstackrc file.
   ::

    cat > /root/openstackrc << EOF
    export OS_USERNAME=admin
    export OS_PASSWORD=password
    export OS_TENANT_NAME=admin
    export OS_AUTH_URL=http://keystone-api.openstack:35357/v3
    # The following lines can be omitted
    #export OS_TENANT_ID=tenantIDString
    #export OS_REGION_NAME=regionName
    export OS_IDENTITY_API_VERSION=3
    export OS_USER_DOMAIN_NAME=${OS_USER_DOMAIN_NAME:-"Default"}
    export OS_PROJECT_DOMAIN_NAME=${OS_PROJECT_DOMAIN_NAME:-"Default"}
    EOF



#. Test the OpenStack client.
   ::

    source openstackrc
    openstack server list
    openstack stack list
    openstack --help




Accessing the Contrail Web UI
-----------------------------


#. Access the Contrail Web UI using port 8143. Use the IP address of the host where the contrail-webui pod is running, with the port 8143.
   ::

    https://<IP address host with contrail-webui>:8143



#. At the Contrail login screen, enter the default username and password: admin, password.




Accessing OpenStack Horizon
----------------------------

The OpenStack Web UI (GUI) service is exposed by the Kubernetes service, using the IP address of the node port and the default port 31000.


#. Check the NodePort used for the OpenStack Web UI pod.
   ::

    kubectl get svc -n openstack | grep horizon-int
    horizon-int           NodePort    10.99.150.28     <none>        80:31000/TCP         4d



#. Access the OpenStack Web UI and log in with the default username and password: admin, password.
   ::

    http://<IP address NodePort>:31000/auth/login/?next=/





Accessing the Virtual Machine Console from Horizon
---------------------------------------------------

To access the virtual machine (VM) console, add the nova novncproxy fully-qualified domain name (FQDN) in the /etc/hosts file, using the host-ip where the osh-ingress pod is running.

The following example for MAC-OS shows the ingress pod running on the host with IP address 10.13.82.233.
   ::

    /private/etc/hosts                                                                                                   
    127.0.0.1	localhost
    255.255.255.255	broadcasthost
    ::1             localhost
    10.13.82.233 nova-novncproxy.openstack.svc.cluster.local


.. note:: If you don't want to make changes in /etc/hosts, you can replace the nova-novncproxy.openstack.svc.cluster.local portion in the URL with the IP address where the OSH ingress pod is running.





OpenStack References
--------------------

For more information about accessing and using OpenStack, see the following OpenStack resources:

-  `Create OpenStack client environment scripts`_  


-  `Install the OpenStack command-line clients`_  


-  `External DNS to FQDN/Ingress`_  


.. _Installing and Managing Contrail 5.0 Microservices Architecture Using Helm Charts: install-microsvcs-helm-chart-50.html

.. _Using Helm Charts to Provision Multinode Contrail OpenStack Ocata with High Availability: install-microsvcs-helm-multi-50.html

.. _Using Helm Charts to Provision All-in-One Contrail with OpenStack Ocata: install-microsvcs-helm-aio-50.html

.. _Frequently Asked Questions About Contrail and Helm Charts: install-microsvcs-helm-multi-faq-50.html


.. _Create OpenStack client environment scripts: https://docs.openstack.org/newton/install-guide-ubuntu/keystone-openrc.html

.. _Install the OpenStack command-line clients: https://docs.openstack.org/newton/user-guide/common/cli-install-openstack-command-line-clients.html

.. _External DNS to FQDN/Ingress: https://docs.openstack.org/openstack-helm/latest/install/ext-dns-fqdn.html
