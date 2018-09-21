.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==========================================================================
Sample Network Configuration for Devices for Simple Tiered Web Application
==========================================================================

This section shows sample device configurations that can be used to create the `Example\:\ Deploying a Multi-Tier Web Application`_ . Configurations are shown for Juniper Networks devices: two MX80s and one EX4200.

*MX80-1 Configuration* 

::

 version 12.2R1.3;
 system {


   root-authentication {

   encrypted-password "xxxxxxxxxx"; ## SECRET-DATA

   }


   services {


     ssh {

     root-login allow;

     }

   }


   syslog {


     user * {

     any emergency;

     }


     file messages {

     any notice;

     authorization info;

     }

   }

 }


 chassis {


   fpc 1 {


     pic 0 {

     tunnel-services;

     }

   }

 }


 interfaces {


   ge-1/0/0 {


     unit 0 {


       family inet {

       address 10.84.11.253/24;

       }

     }

   }


   ge-1/1/0 {

   description "IP Fabric interface";


     unit 0 {


       family inet {

       address 10.84.45.1/24;

       }

     }

   }


   lo0 {


     unit 0 {


       family inet {

       address 127.0.0.1/32;

       }

     }

   }

 }


 routing-options {


   static {

   route 0.0.0.0/0 next-hop 10.84.45.254;

   }

 route-distinguisher-id 10.84.11.253;

 autonomous-system 64512;


   dynamic-tunnels {


     setup1 {

     source-address 10.84.11.253;

     gre;


       destination-networks {

       10.84.11.0/24;

       }

     }

   }

 }


 protocols {


   bgp {


     group mx {

     type internal;

     local-address 10.84.11.253;


       family inet-vpn {

       unicast;

       }

     neighbor 10.84.11.252;

     }


     group contrail-controller {

     type internal;

     local-address 10.84.11.253;


       family inet-vpn {

       unicast;

       }

     neighbor 10.84.11.101;

     neighbor 10.84.11.102;

     }

    

   }

 }


 routing-instances {


   customer-public {

   instance-type vrf;

   interface ge-1/1/0.0;

   vrf-target target:64512:10000;


     routing-options {


       static {

       route 0.0.0.0/0 next-hop 10.84.45.254;

       }

     }

   }

 }

*MX80-2 Configuration* 

::

 version 12.2R1.3;
 system {


   root-authentication {

   encrypted-password "xxxxxxxxx"; ## SECRET-DATA

   }


   services {


     ssh {

     root-login allow;

     }

   }


   syslog {


     user * {

     any emergency;

     }


     file messages {

     any notice;

     authorization info;

     }

   }

 }


 chassis {


   fpc 1 {


     pic 0 {

     tunnel-services;

     }

   }

 }


 interfaces {


   ge-1/0/0 {


     unit 0 {


       family inet {

       address 10.84.11.252/24;

       }

     }

   }


   ge-1/1/0 {

   description "IP Fabric interface";


     unit 0 {


       family inet {

       address 10.84.45.2/24;

       }

     }

   }


   lo0 {


     unit 0 {


       family inet {

       address 127.0.0.1/32;

       }

     }

   }

 }


 routing-options {


   static {

   route 0.0.0.0/0 next-hop 10.84.45.254;

   }

 route-distinguisher-id 10.84.11.252;

 autonomous-system 64512;


   dynamic-tunnels {


     setup1 {

     source-address 10.84.11.252;

     gre;


       destination-networks {

       10.84.11.0/24;

       }

     }

   }

 }


 protocols {


   bgp {


     group mx {

     type internal;

     local-address 10.84.11.252;


       family inet-vpn {

       unicast;

       }

     neighbor 10.84.11.253;

     }


     group contrail-controller {

     type internal;

     local-address 10.84.11.252;


       family inet-vpn {

       unicast;

       }

     neighbor 10.84.11.101;

     neighbor 10.84.11.102;

     }

    

   }

  

 }


 routing-instances {


   customer-public {

   instance-type vrf;

   interface ge-1/1/0.0;

   vrf-target target:64512:10000;


     routing-options {


       static {

       route 0.0.0.0/0 next-hop 10.84.45.254;

       }

     }

   }

 }

*EX4200 Configuration* 

::

 system {

 host-name EX4200;

 time-zone America/Los_Angeles;


   root-authentication {

   encrypted-password "xxxxxxxxxxxxx"; ## SECRET-DATA

   }


   login {


     class read {

     permissions [ clear interface view view-configuration ];

     }


     user admin {

     uid 2000;

     class super-user;


       authentication {

       encrypted-password "xxxxxxxxxxxx"; ## SECRET-DATA

       }

     }


     user user1 {

     uid 2002;

     class read;


       authentication {

       encrypted-password "xxxxxxxxxxxxxx"; ## SECRET-DATA

       }

     }

   }


   services {


     ssh {

     root-login allow;

     }

   telnet;


     netconf {

     ssh;

     }


     web-management {

     http;

     }

   }


   syslog {


     user * {

     any emergency;

     }


     file messages {

     any notice;

     authorization info;

     }


     file interactive-commands {

     interactive-commands any;

     }

   }

 }


 chassis {


   aggregated-devices {


     ethernet {

     device-count 64;

     }

   }

 }

.. _Example\:\ Deploying a Multi-Tier Web Application: web-use-case-vnc.html

