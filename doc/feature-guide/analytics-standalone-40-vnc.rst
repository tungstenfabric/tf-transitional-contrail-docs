.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

==============================================
Configuring Analytics as a Standalone Solution
==============================================

Starting with Contrail 4.0, it is possible to configure Contrail Analytics as a standalone solution.

-  `Overview: Contrail Analytics as a Standalone Solution`_ 


-  `Configuration Examples for Standalone`_ 




Overview: Contrail Analytics as a Standalone Solution
-----------------------------------------------------

Starting with Contrail 4.0 (containerized Contrail), Contrail Analytics can be configured as a standalone solution.

The following services are necessary for a standalone solution:

- config


- webui


- analytics


- analyticsdb


A standalone Contrail Analytics solution consists of the following containers:

- controller container with only config and webui services enabled


- analytics container


- analyticsdb container




Configuration Examples for Standalone
-------------------------------------

The following are examples of default inventory file configurations for the controller container for standalone Contrail analytics.

-  `Examples: Inventory File Controller Components`_ 


-  `JSON Configuration Examples`_ 




Examples: Inventory File Controller Components
-----------------------------------------------

The following are example analytics standalone solution inventory file configurations for Contrail controller container components.

-  `Single Node Cluster`_ 


-  `Multi-Node Cluster`_ 




Single Node Cluster
-------------------


::

 [contrail-controllers]
 10.xx.32.10             controller_components=['config','webui']

 [contrail-analyticsdb]
 10.xx.32.10

 [contrail-analytics]
 10.xx.32.10




Multi-Node Cluster
------------------



::

 [contrail-controllers]
 10.xx.32.10             controller_components=['config','webui']
 10.xx.32.11             controller_components=['config','webui']
 10.xx.32.12             controller_components=['config','webui']

 [contrail-analyticsdb]
 10.xx.32.10
 10.xx.32.11
 10.xx.32.12

 [contrail-analytics]
 10.xx.32.10
 10.xx.32.11
 10.xx.32.12




JSON Configuration Examples
---------------------------

The following are example JSON file configurations for (  server.json) for Contrail analytics standalone solution.

-  `Example: JSON Single Node Cluster`_ 


-  `Example: JSON Multi-Node Cluster`_ 




Example: JSON Single Node Cluster
---------------------------------


::

 {                                                                
     "cluster_id": "cluster1",                                    
     "domain": "sm-domain.com",                                   
     "id": "server1",                                             
     "parameters" : {                                             
         "provision": {                                           
             "contrail_4": {                                      
                "controller_components": "['config',’webui']"   
             },                  
     …
     …
 }




Example: JSON Multi-Node Cluster
--------------------------------


::

 {                                                                
     "cluster_id": "cluster1",                                    
     "domain": "sm-domain.com",                                   
     "id": "server1",                                             
     "parameters" : {                                             
         "provision": {                                           
             "contrail_4": {                                      
                "controller_components": "['config',’webui']"   
             },                  
     …
     …
 },
 {                                                                
     "cluster_id": "cluster1",                                    
     "domain": "sm-domain.com",                                   
     "id": "server2",                                             
     "parameters" : {                                             
         "provision": {                                           
             "contrail_4": {                                      
                "controller_components": "['config',’webui']"   
             },                  
     …
     …
 },
 {                                                                
     "cluster_id": "cluster1",                                    
     "domain": "sm-domain.com",                                   
     "id": "server3",                                             
     "parameters" : {                                             
         "provision": {                                           
             "contrail_4": {                                      
                "controller_components": "['config',’webui']"   
             },                  
     …
     …
 }



**Related Documentation**

-  `Configuring Secure Sandesh and Introspect for Contrail Analytics`_ 

-  `Understanding Contrail Analytics`_ 

.. _Configuring Secure Sandesh and Introspect for Contrail Analytics: analytics-secure-sandesh-40-vnc.html

.. _Understanding Contrail Analytics: analytics-overview-vnc.html

