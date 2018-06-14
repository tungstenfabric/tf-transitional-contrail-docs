.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

================================
Supported Platforms Contrail 5.0
================================

`Table 1`_ lists the orchestrator releases and the corresponding operating systems and kernel versions supported by Contrail Release 5.0.

.. _Table 1: 

*Table 1* : Supported Platforms

 +-----------------------+----------------------+-----------------+-----------------------------------------------------------------------------+
 | Contrail Release      | Orchestrator Release | Deployment Tool | Operating System, Kernel, and Key components version                        |
 +=======================+======================+=================+=============================================================================+
 | Contrail Release 5.0  | Kubernetes 1.9.2     | Ansible         | - CentOS 7.4—Linux Kernel Version 1.10.0-691.21.1 Docker version: 17.01.1-ce|
 +-----------------------+----------------------+-----------------+-----------------------------------------------------------------------------+
 |                       | Openshift 1.7        | Ansible         | - CentOS 7.4—Linux Kernel Version 1.10.0-691.21.1                           |
 |                       |                      |                 |   Ansible version: 2.5.1 Docker version: 1.12.6                             |
 +-----------------------+----------------------+-----------------+-----------------------------------------------------------------------------+
 |                       | OpenStack Ocata      | Ansible         | - CentOS 7.4—Linux Kernel Version 1.10.0-691.21.1                           |
 |                       |                      |                 |   Ansible version: 2.4.2 Docker version: 17.01.1-ce                         |
 |                       |                      +-----------------+-----------------------------------------------------------------------------+
 |                       |                      | Helm            | - Ubuntu 16.04.1—Linux Kernel Version 4.4.0-87                              |
 |                       |                      |                 |   Docker version: 1.11.1 Helm version: 2.7.2 Kubernetes version: 1.9.1      |
 +-----------------------+----------------------+-----------------+-----------------------------------------------------------------------------+
 |                       | VMware vCenter 6.5   | Ansible         | - ESX version 6.5 CentOS VM version running vRouter:                        |
 |                       |                      |                 |   CentOS 7.4—Linux Kernel Version 1.10.0-691.21.1                           |
 +-----------------------+----------------------+-----------------+-----------------------------------------------------------------------------+

