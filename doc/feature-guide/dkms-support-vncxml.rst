.. This work is licensed under the Creative Commons Attribution 4.0 International License.
   To view a copy of this license, visit http://creativecommons.org/licenses/by/4.0/ or send a letter to Creative Commons, PO Box 1866, Mountain View, CA 94042, USA.

================================================
Dynamic Kernel Module Support (DKMS) for vRouter
================================================

Dynamic Kernel Module Support (DKMS) is a framework provided by Linux to automatically build out-of-tree driver modules for Linux kernels whenever the Linux distribution upgrades the existing kernel to a newer version.

In Contrail, the vRouter kernel module is an out-of-tree, high performance packet forwarding module that provides advanced packet forwarding functionality in a reliable and stable manner. Contrail provides a DKMS-compatible source package for Ubuntu so that if you deploy an Ubuntu-based Contrail system you do not need to manually compile the kernel module each time the Linux deployment gets upgraded.

The ``contrail-vrouter-dkms`` package provides the DKMS compatibility for Contrail. Prior to installing the ``contrail-vrouter-dkms`` package, you must install both the DKMS package and the ``contrail-vrouter-utils`` package, because the ``contrail-vrouter-dkms`` package is dependent on both. Installing the ``contrail-vrouter-dkms`` package adds the vRouter sources to the DKMS database, builds the vRouter module, and installs it in the existing kernel modules tree. When a kernel upgrade occurs, DKMS ensures that the module is compiled for the newer kernel and installed in the proper location so that upon reboot, the newer module can be used with the upgraded kernel.

For more information about DKMS, refer to:

- DKMS Ubuntu documentation at https://help.ubuntu.com/community/DKMS


- DKMS Ubuntu manual pages at http://manpages.ubuntu.com/manpages/lucid/man8/dkms.8.html


- Linux Journal article on DKMS at http://www.linuxjournal.com/article/6896 
