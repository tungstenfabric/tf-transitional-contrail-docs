.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

================================
Configuring Multitenancy Support
================================

The following sections describe enabling and viewing multitenancy support.

-  `Multitenancy Permissions`_ 


-  `API Server`_ 


-  `API Library Keystone Integration`_ 


-  `Supporting Utilities`_ 




Multitenancy Permissions
------------------------

The multi tenancy feature of the API server enables multiple tenants to coexist on the system without interfering with each other. This is achieved by encoding ownership information and permissions with each resource, allowing fine-grained control over create, read, update, and delete (CRUD) operations on those resources.

The Contrail ``api-server`` enforces resources permissions in a manner similar to Unix files. Each resource has an owner and group. Permissions associated with owner, group, and "others" are:

-  ``R`` - reading resource


-  ``W`` - create/update resource


-  ``X`` - link (refer to) object


CRUD permission requirements for resources managed by ``api-server`` are as follows:

-  ``C`` - write on parent object

For example, to create a virtual network requires write permission on the project.


-  ``R`` - read on object (parent if a collection)


-  ``U`` - write on object


-  ``D`` - write on parent


-  ``ref(link)`` - execute on object

For example, on a virtual network using ``network-ipam`` , ``network-ipam`` should have X permissions for owner, group, or "others".




API Server
----------

If multitenancy is enabled, ``api-server`` deploys keystone middleware in its pipeline. The keystone middleware architecture supports a common authentication protocol in use between OpenStack projects.

The keystone middleware works in conjunction with ``api-server`` to derive the user name and role for each incoming request. Once obtained, the user name and role are matched against resource ownership and permissions. If the ownership matches or the permissions allow access, access is granted.

For example, assume Tenant A has the following attributes:

- owner = Bob


- group = Staff


- permisssions = 750


In this example, only Bob can create a virtual network in Tenant A. Other staff members can view the virtual networks in Tenant A. No others can create or view any virtual networks in Tenant A.

Clients can obtain an ``auth_token`` by posting credentials to the keystone admin API ``(/v2.0/tokens`` ). The ``VncApi`` client library does this automatically. If an ``auth_token`` is present in an incoming request, ``api-server`` validates credentials derived from the token against object permissions. If an incoming request has an invalid or missing ``auth_token`` , a 401 error is returned.

Notes:

- Multitenancy is enabled by the flag ``multi_tenancy``   ``in /etc/contrail/api-server.conf`` 


- If multitenancy is enabled, ``memcaching`` is automatically enabled, to improve token validation response time.




API Library Keystone Integration
--------------------------------

``VncApi`` has been updated to check for any 401 error that ``api-server`` returns as a result of a missing or invalid token. This forces ``VncApi`` to connect with the keystone middleware and fetch an ``auth_token`` . All subsequent requests to ``api-server`` include the ``auth_token`` .



Supporting Utilities
--------------------

-  ``/opt/contrail/utils/chmod.py`` —- To change permissions and ownership (user or group membership) of a resource. Requires the resource type (for example, ``virtual-network`` ) and the resource FQN (for example, ``default-domain:default-project:default-virtual-network`` ).

Invoke python /opt/contrail/utils/chmod.py -h to see usage information

Example 1 - See current permissions:

::

 [root@host]# python /opt/contrail/utils/chmod.py <ip address> project default-domain:default-project 
 Type =  project   
 Name =  default-domain:default-project   
 API Server =  <ip address>   
 Keystone credentials admin/<password>/admin   
 Obj uuid =  6765f112-938f-4251-b3a9-fbbdcc09db18   
 Obj perms = cloud-admin/cloud-admin-group 777    

 [root@host]# python /opt/contrail/utils/chmod.py <ip address> --owner foo --group bar --perms 555 project default-domain:default-project   
 Type =  project   Name =  default-domain:default-project   
 API Server =  <ip address>   
 Owner =  foo   
 Group =  bar   
 Perms =  555   
 Keystone credentials admin/<password>/admin   
 Obj uuid =  6765f112-938f-4251-b3a9-fbbdcc09db18   
 Obj perms = cloud-admin/cloud-admin-group 777  
  New perms = foo/bar 555


-  ``/opt/contrail/utils/multi_tenancy.py`` —- Show if multitenancy is enabled or disabled. Also used to turn multitenancy on or off. Requires admin credentials.
   Invoke python /opt/contrail/utils/multi_tenancy.py -h to see usage information
   Example 1: View multitenancy status:

::

 [root@host]# python /opt/contrail/utils/multi_tenancy.py <ip address>
 API Server =  <ip address>   
 Keystone credentials admin/<password>/admin   

 Multi Tenancy is enabled


Example 2: Turn multitenancy off:

::

 [root@host]# python /opt/contrail/utils/multi_tenancy.py <ip address>--off
 API Server =  <ip address>
 Keystone credentials admin/<password>/admin

 Multi Tenancy is disabled




