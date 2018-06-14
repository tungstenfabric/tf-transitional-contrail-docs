.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

=========================================================================================
Sample JSON Configuration Files for vCenter with Containerized Contrail 4.0.1 and Greater
=========================================================================================

Starting with Contrail Release 4.0.1, vCenter can be used with containerized Contrail. This section presents sample JSON files that can be used to provision containerized Contrail using Server Manager. Be sure to replace parameters in the samples with values specific to your system.

-  `Sample Image JSON for vCenter-Only Mode`_ 


-  `Sample Cluster JSON for vCenter-Only Mode`_ 


-  `Sample Server JSON for vCenter-Only Mode`_ 


-  `Sample JSON for vCenter-only with High Availability`_ 


-  `Sample Image JSON for vCenter-as-Compute Mode`_ 


-  `Sample Cluster JSON for vCenter-as-Compute Mode`_ 


-  `Sample Server JSON for vCenter-as-Compute Mode`_ 



Sample Image JSON for vCenter-Only Mode
=======================================
::

     {
 "image": [
     {   
         "category": "package",
         "id": "contrail_vc_orch",
         "path": "/root/contrail-vcenter-docker_4.0.1.0-50_trusty.tgz",
         "type": "contrail-ubuntu-package",
         "parameters": {"openstack_sku": "vcenter"},
         "version": "4.0.1.0-50"
     }
 ]
 }



Sample Cluster JSON for vCenter-Only Mode
=========================================
::

    {
 "cluster": [
     {
         "id": "cluster-esxi-new", 
         "parameters": {
             "provision": {
                 "contrail": {
                 }, 
                 "contrail_4": {
                     "cloud_orchestrator": "vcenter", 
                     "vcenter_servers": [
                         {
                             "server1": {
                                 "datacenters": {
                                     "kp_datacenter11": {
                                         "datacenter_mtu": 1500, 
                                         "dv_switch_control_data": {
                                             "dv_port_group_control_data": {
                                                 "dv_portgroup_name": "", 
                                                 "number_of_ports": "", 
                                                 "uplink": ""
                                             }, 
                                             "dv_switch_name": ""
                                         }, 
                                         "dv_switch_mgmt": {
                                             "dv_port_group_mgmt": {
                                                 "dv_portgroup_name": "", 
                                                 "number_of_ports": "", 
                                                 "uplink": ""
                                             }, 
                                             "dv_switch_name": ""
                                         }, 
                                         "dv_switches": [
                                             {
                                                 "clusternames": [
                                                     "kp_cluster11", 
                                                     "kp_cluster12"
                                                 ], 
                                                 "dv_port_group": {
                                                     "dv_portgroup_name": "vm_dvs_pg2", 
                                                     "number_of_ports": "3"
                                                 }, 
                                                 "dv_switch_name": "vm_dvs2", 
                                             }
                                         ]
                                     }
                                 }, 
                                 "hostname": "10.xx.x.76", 
                                 "password": "<password>", 
                                 "username": "administrator@vsphere.local", 
                                 "validate_certs": false
                             }
                         }
                     ]
                 }
             }
         }
     }
 ]
 }



Sample Server JSON for vCenter-Only Mode
========================================
::

    {
 "server": [
     {
         "cluster_id": "cluster-esxi-new", 
         "contrail": {
             "control_data_interface": "eth1"
         }, 
         "domain": "contrail.juniper.net", 
         "host_name": "controller1-b7s28", 
         "id": "controller1-b7s28", 
         "network": {
             "interfaces": [
                 {
                     "dhcp": true, 
                     "ip_address": "10.xx.xx.59", 
                     "mac_address": "00:50:56:a6:47:72", 
                     "default_gateway": "10.xx.xx.254",
                     "name": "eth0"
                 }, 
                 { 
                     "dhcp": false, 
                     "ip_address": "192.xxx.xxx.101/24", 
                     "mac_address": "00:50:56:a6:4d:38", 
                     "name": "eth1"
                 }
             ], 
             "management_interface": "eth0"
         }, 
         "password": "<password>", 
         "roles": [
             "contrail-controller", 
             "contrail-analytics", 
             "contrail-analyticsdb", 
             "contrail-vcenter-plugin"
         ]
     }, 
     {
         "cluster_id": "cluster-esxi-new", 
         "contrail": {
             "control_data_interface": "eth1"
         }, 
         "domain": "contrail.juniper.net", 
         "host_name": "computevm-b7s28", 
         "id": "computevm-b7s28", 
         "ip_address": "10.xx.xx.54", 
         "network": {
             "interfaces": [
                 {
                     "dhcp": true, 
                     "ip_address": "10.xx.xx.54", 
                     "mac_address": "00:50:56:05:ba:ba",
                     "default_gateway": "10.xx.x.254",
                     "name": "eth0"
                 }, 
                 {
                     "dhcp": false, 
                     "ip_address": "192.xxx.xxx.28/24", 
                     "mac_address": "00:50:56:05:bb:bb", 
                     "name": "eth1"
                 }
             ], 
             "management_interface": "eth0"
         }, 
         "parameters": {
             "esxi_parameters": {
                 "cluster": "kp_cluster11", 
                 "contrail_vm": {
                     "control_data_pg": "control_data", 
                     "control_data_switch": "vSwitch1", 
                     "mgmt_pg": "mgmt-pg", 
                     "vmdk": "/root/vmdk/vmdk.tar"
                 }, 
                 "datacenter": "kp_datacenter11", 
                 "datastore": "datastore1", 
                 "name": "10.xx.xx.28", 
                 "password": "<password>", 
                 "username": "root", 
                 "validate_certs": false, 
                 "vcenter_server": "server1"
             }
         }, 
         "password": "<password>", 
         "roles": [
             "contrail-compute"
         ]
     }
 ]
 }



Sample JSON for vCenter-only with High Availability
===================================================
::

    {
    "cluster": [{
            "id": "vcenter_cluster",
            "parameters": {
                "provision": {
                    "contrail_4": {
                        "cloud_orchestrator": "vcenter",
                        "vcenter_servers": [
                        {
                            "<your.server.company.net>": {
                                "datacenters": {
                                    "Cluster": {
                                        "datacenter_mtu": 1500, 
                                        "dv_switches": [
                                            {
                                                "clusternames": [
                                                    "contrail-csg2"
                                                ], 
                                                "dv_port_group": {
                                                    "dv_portgroup_name": "dv-portgroup", 
                                                    "number_of_ports": "3"
                                                }, 
                                                "dv_switch_name": "dvs-switch" 
                                            }
                                        ]
                                    }
                                }, 
                                "hostname": "10.xx.xx.xxx", 
                                "password": "<password>!", 
                                "username": "administrator@vsphere.local", 
                                "validate_certs": false
                            }
                        }],
                    "ha":  
                    {
                       "contrail_external_vip": "10.12.34.1",
                       "contrail_internal_vip": "10.12.34.1"
                    }
                }
            }
        }
    }
    ],
    "server": [{
            "cluster_id": "vcenter_cluster",
            "contrail": {},
            "domain": "<domain-name.company.net>",
            "host_name": "<hostname>",
            "id": "<hostname>",
            "network": {
                "interfaces": [{
                    "default_gateway": "10.xx.xx.254",
                    "dhcp": true,
                    "ip_address": "10.xx.xx.152/24",
                    "mac_address": "00:0c:29:99:77:45",
                    "name": "eth0"
                }],
                "management_interface": "eth0"
            },
            "parameters": {},
            "password": "<password>",
            "roles": [
                "contrail-controller",
                "contrail-analytics",
                "contrail-analyticsdb",
                "contrail-vcenter-plugin"
            ]
        },
        {
            "cluster_id": "vcenter_cluster",
            "contrail": {},
            "domain": "<domain-name.company.net>",
            "host_name": "<hostname>",
            "id": "<hostname>",
            "network": {
                "interfaces": [{
                    "default_gateway": "10.xx.xx.254",
                    "dhcp": true,
                    "ip_address": "10.xx.xx.155/24",
                    "mac_address": "00:0c:29:38:6d:5d",
                    "name": "eth0"
                }],
                "management_interface": "eth0"
            },
            "parameters": {},
            "password": "<password>",
            "roles": [
                "contrail-controller",
                "contrail-analytics",
                "contrail-analyticsdb",
                "contrail-vcenter-plugin"
            ]
        },
        {
            "cluster_id": "vcenter_cluster",
            "contrail": {},
            "domain": "<domain-name.company.net>",
            "host_name": "<hostname>",
            "id": "<id-name>",
            "network": {
                "interfaces": [{
                    "default_gateway": "10.xx.xx.254",
                    "dhcp": true,
                    "ip_address": "10.xx.xx.156/24",
                    "mac_address": "00:0c:29:ea:37:33",
                    "name": "eth0"
                }],
                "management_interface": "eth0"
            },
            "parameters": {},
            "password": "<password>",
            "roles": [
                "contrail-controller",
                "contrail-analytics",
                "contrail-analyticsdb",
                "contrail-vcenter-plugin"
            ]
        },
        {
            "cluster_id": "vcenter_cluster",
            "contrail": {},
            "domain": "<domain-name.company.net>",
            "host_name": "<hostname>",
            "id": "<id-name>",
            "network": {
                "interfaces": [{
                    "default_gateway": "10.xx.xx.254",
                    "dhcp": true,
                    "ip_address": "10.xx.xx.1/24",
                    "mac_address": "08:9e:01:93:cb:e0",
                    "name": "em1"
                }],
                "management_interface": "em1"
            },
            "parameters": {},
            "password": "<password>",
            "roles": [
                "contrail-lb"
            ]
        },
        {
            "cluster_id": "vcenter_cluster",
            "contrail": {},
            "domain": "<domain-name.company.net>",
            "host_name": "<hostname>",
            "id": "<id-name>",
            "network": {
                "interfaces": [{
                    "default_gateway": "10.xx.xx.254",
                    "dhcp": true,
                    "ip_address": "10.xx.xx.153/24",
                    "mac_address": "00:50:56:05:ba:b5",
                    "name": "eth0"
                }],
                "management_interface": "eth0"
            },
            "parameters": {
                "esxi_parameters": {
                    "cluster": "contrail-csg2",
                    "contrail_vm": {
                        "mgmt_pg": "mgmt-pg",
                        "vmdk": "/var/tmp/ContrailVM1604-ovf.tar"
                    },
                    "datacenter": "Cluster",
                    "datastore": "datastore1",
                    "name": "10.xx.xx.41",
                    "password": "<password>",
                    "username": "root",
                    "validate_certs": false,
                    "vcenter_server": "<hostname.domain-name.company.net>"
                }
            },
            "password": "<password>",
            "roles": [
                "contrail-compute"
            ]
        },
        {
            "cluster_id": "vcenter_cluster",
            "contrail": {},
            "domain": "<domain-name.company.net>",
            "host_name": "<hostname>",
            "id": "<id-name>",
            "network": {
                "interfaces": [{
                    "default_gateway": "10.xx.xx.254",
                    "dhcp": true,
                    "ip_address": "10.xx.xx.154/24",
                    "mac_address": "00:50:56:05:ce:c5",
                    "name": "eth0"
                }],
                "management_interface": "eth0"
            },
            "parameters": {
                "esxi_parameters": {
                    "cluster": "contrail-csg2",
                    "contrail_vm": {
                        "mgmt_pg": "mgmt-pg",
                        "vmdk": "/var/tmp/ContrailVM1604-ovf.tar"
                    },
                    "datacenter": "Cluster",
                    "datastore": "datastore2",
                    "name": "10.xx.xx.42",
                    "password": "<password>",
                    "username": "root",
                    "validate_certs": false,
                    "vcenter_server": "<hostname.domain-name.company.net>"
                }
            },
            "password": "<password>",
            "roles": [
                "contrail-compute"
            ]
        }
    ],
    "image": [{
        "category": "package",
        "id": "contrail_vc_orch",
        "path": "/var/tmp/contrail-vcenter-docker_4.1.0.0-33_xenial.tgz",
        "type": "contrail-ubuntu-package",
        "parameters": {
            "openstack_sku": "vcenter"
        },
        "version": "4.1.0.0-33"
    }]
 }



Sample Image JSON for vCenter-as-Compute Mode
=============================================
::

    {
 "image": [
     {   
         "category": "package",
         "id": "contrail_vc_compute",
         "path": "/root/contrail-cloud-docker_4.0.1.0-39-mitaka_trusty.tgz",
         "type": "contrail-ubuntu-package",
         "version": "4.0.1.0-39"                     
     }
 ]
 }



Sample Cluster JSON for vCenter-as-Compute Mode
===============================================
::

    {
  "cluster": [
    {
        "id": "vcenter_five_node", 
        "parameters": {
            "provision": {
                "contrail": {
                },
                "contrail_4": {
                    "vcenter_servers": [
                        {
                            "server1": {
                                "datacenters": {
                                    "vc_datacenter1": {
                                        "datacenter_mtu": 1500, 
                                        "dv_switch_control_data": {
                                            "dv_port_group_control_data": {
                                                "dv_portgroup_name": "", 
                                                "number_of_ports": "", 
                                                "uplink": ""
                                            }, 
                                            "dv_switch_name": ""
                                        }, 
                                        "dv_switch_mgmt": {
                                            "dv_port_group_mgmt": {
                                                "dv_portgroup_name": "", 
                                                "number_of_ports": "", 
                                                "uplink": ""
                                            }, 
                                            "dv_switch_name": ""
                                        }, 
                                        "dv_switches": [
                                            {
                                                "clusternames": [
                                                    "vcenter1"
                                                ], 
                                                "dv_port_group": {
                                                    "dv_portgroup_name": "guest_dvs_pg", 
                                                    "number_of_ports": "3"
                                                }, 
                                                "dv_switch_name": "guest_vm_dvs", 
                                                "vcenter_compute": "10.xx.x.205"
                                            }
                                        ]
                                    }
                                }, 
                                "hostname": "10.xx.x.76", 
                                "password": "<password>", 
                                "username": "administrator@vsphere.local", 
                                "validate_certs": false
                            }
                        }
                    ]
                }, 
                "openstack": {
                }
            }
        }
    }
  ]
 }



Sample Server JSON for vCenter-as-Compute Mode
==============================================
::

    {
 "server": [
     {
         "cluster_id": "vcenter_five_node", 
         "contrail": {}, 
         "domain": "contrail.juniper.net", 
         "gateway": "10.xx.x.254", 
         "host_name": "nk-vm1", 
         "id": "nk-vm1", 
         "network": {
             "interfaces": [
                 {
                     "default_gateway": "10.xx.x.254", 
                     "ip_address": "10.xx.x.202/24", 
                     "mac_address": "52:54:DE:AD:BD:A1", 
                     "name": "eth1"
                 }
             ], 
         }, 
         "password": "<password>", 
         "roles": [
             "contrail-controller", 
             "contrail-analytics", 
             "contrail-analyticsdb"
         ]
     }, 
     {
         "cluster_id": "vcenter_five_node", 
         "contrail": {}, 
         "domain": "contrail.juniper.net", 
         "host_name": "nk-vm2", 
         "id": "nk-vm2", 
         "network": {
             "interfaces": [
                 {
                     "default_gateway": "10.xx.x.254", 
                     "ip_address": "10.xx.x.203/24", 
                     "mac_address": "52:54:DE:AD:BD:A2", 
                     "name": "eth1"
                 }
             ]
         }, 
         "password": "<password>", 
         "roles": [
             "openstack"
         ]
     }, 
     {
         "cluster_id": "vcenter_five_node", 
         "contrail": {}, 
         "domain": "contrail.juniper.net", 
         "host_name": "nk-vm3", 
         "id": "nk-vm3", 
         "network": {
             "interfaces": [
                 {
                     "default_gateway": "10.xx.x.254", 
                     "ip_address": "10.xx.x.204/24", 
                     "mac_address": "52:54:DE:AD:BD:A3", 
                     "name": "eth1"
                 }
             ]
         }, 
         "password": "<password>", 
         "roles": [
             "contrail-vcenter-plugin"
         ]
     }, 
     {
         "cluster_id": "vcenter_five_node", 
         "contrail": {}, 
         "domain": "contrail.juniper.net", 
         "host_name": "nk-vm4", 
         "id": "nk-vm4", 
         "network": {
             "interfaces": [
                 {
                     "default_gateway": "10.xx.x.254", 
                     "ip_address": "10.xx.x.205/24", 
                     "mac_address": "52:54:DE:AD:BD:A4", 
                     "name": "eth1"
                 }
             ]
         }, 
         "password": "<password>", 
         "roles": [
             "contrail-vcenter-compute"
         ]
     }, 
     {
         "cluster_id": "vcenter_five_node", 
         "contrail": {}, 
         "domain": "contrail.juniper.net", 
         "host_name": "computevm-b7s27", 
         "id": "computevm-b7s27", 
         "network": {
             "interfaces": [
                 {
                     "default_gateway": "10.xx.xx.254", 
                     "dhcp": true, 
                     "ip_address": "10.xx.xx.57/24", 
                     "mac_address": "00:50:56:AD:BD:A5", 
                     "name": "eth1"
                 }
             ]
         }, 
         "parameters": {
             "esxi_parameters": {
                 "cluster": "vcenter1", 
                 "contrail_vm": {
                     "mgmt_pg": "mgmt-pg", 
                     "mode": "vcenter", 
                     "vmdk": "/root/vmdk/vmdk.tar"
                 }, 
                 "datacenter": "vc_datacenter1", 
                 "datastore": "datastore1", 
                 "name": "10.xx.xx.27", 
                 "password": "<password>", 
                 "username": "root", 
                 "validate_certs": false, 
                 "vcenter_server": "server1"
             }
         }, 
         "password": "<password>", 
         "roles": [
             "contrail-compute"
         ]
     }
 ]
 }


**Related Documentation**

-  `Installing and Provisioning VMware vCenter with Containerized Contrail`_ 

-  `Underlay Network Configuration for Containerized ContrailVM`_ 

.. _Installing and Provisioning VMware vCenter with Containerized Contrail: vcenter-integration-vnc-401.html

.. _Underlay Network Configuration for Containerized ContrailVM: vcenter-as-compute-deployment-scenarios-401.html

