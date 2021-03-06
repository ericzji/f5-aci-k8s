************
Requirements
************

Required Hardware
===================

One ACI fabric with at least:

#. APIC
#. Spine (any model)
#. Leaves -EX or newer the Plugin will not work with first Generation leaves
#. ESXi Server with vCenter

Software Version
================
Please refer to https://www.cisco.com/c/dam/en/us/td/docs/Website/datacenter/aci/virtualization/matrix/virtmatrix.html for the latest information. 

As for this lab I assume 

#.	ACI 3.2.x 
#.	ACI CNI 4.1
#.	Ubuntu 16
#.	Kubernetes 1.13

Connectivity and ACI pre-requisites:
=====================================
VMware VMM integration:

#.	ACI must be integrated with vCenter with dVS
#.	Each ESXi host MUST be connected to the fabric via Virtual Port-Channel 


.. Warning::
    Standalone ESXi hosts with Standard vSwitch are not officially supported. They can be made to work but it requires manual configuration for the port-group with specific requirements. From experience things will break and you will lose hours on this. So please just use VMM integration with vCenter. 

If you want to deviate from the above assumption you can use Bare Metal hosts please refer to this link for the connectivity requirements:
https://www.cisco.com/c/en/us/td/docs/switches/datacenter/aci/apic/sw/kb/b_Cisco_ACI_and_OpFlex_Connectivity_for_Orchestrators.html

.. Warning::
    Deviating from the connectivity requirements will result in a broken/non-      working cluster.  

ACI L3 OUT and VRF
===================
For the purposes of this lab we will deploy everything in a dedicated tenant. 
The VRF, BD, Service Graphs and L3OUT will be all within our tenant. 

.. note::
    It is possible to place the network component in the common tenant and share a L3OUT in common but is a more advance config and is not covered in this guide

Ubuntu Virtual Machines
========================
Install at latest two Ubuntu 16.x VMs and configure them with a single network interface. This interface will point to the ACI fabric as default gateway. 

This will require the ACI fabric tenant to be pre-provisioned with the required VRFs/EPGs/L3OUTs. 

.. Warning::
    It is possible to have a NIC for management. If you choose to do so however the default gateway MUST be ACI. Deviating from this requirement will most likely result in a broken cluster. 
