.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

========================================
ECMP Load Balancing in the Service Chain
========================================



Traffic flowing through a service chain can be load-balanced by distributing traffic streams to multiple service virtual machines (VMs) that are running identical applications. This is illustrated in `Figure 53`_ , where the traffic streams between VM-A and VM-B are distributed between Service VM-1 and Service VM-2. If Service VM-1 goes down, then all streams that are dependent on Service VM-1 will be moved to Service VM-2.

.. _Figure 53: 

*Figure 53* : Load Balancing a Service Chain

 .. figure:: s041830.gif

The following are the major features of load balancing in the service chain:

- Load balancing can be configured at every level of the service chain.


- Load balancing is supported in routed and bridged service chain modes.


- Load balancing can be used to achieve high availability—if a service VM goes down, the traffic passing through that service VM can be distributed through another service VM.


- A load balanced traffic stream always follows the same path through the chain of service VM.


**Related Documentation**

-  `Service Chaining`_ 

-  `Customized Hash Field Selection for ECMP Load Balancing`_ 

.. _Service Chaining: service-chaining-vnc.html

.. _Customized Hash Field Selection for ECMP Load Balancing: custom-field-hash-vnc.html

