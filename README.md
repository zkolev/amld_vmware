## Problem description

As two of the most-mature products, vSphere and vCenter Server provides great deal of customization and flexibility. However, given the complexity of the modern virtualization and the numerous different technologies involved in modern computing network and storage it the customization options for VM Ware products grew infusible large for common system administrators to grasp.

At the same time different workloads have different needs. Given that virtually there is always a tradeoff between different functionalities of the system (like throughput and security, performance and redundancy) unfortunately, there is not one configuration to serve equally well all kind of workloads. Understanding the purpose of the environment is crucial for the proper reconfiguration. 

Wile it is easy to profile single virtual machine, VMWare's software hosts tens of millions virtual environments. Thus in order to approach their need proactively we need to find a data driven way to classify them in terms of their properties.  
</br> 

### The Challenge 

VSphere stack allows us to collect on demand low level performance telemetry. Based on this data we need to identify groups of virtual machines similar with respect to their properties, such as scale, utilization pattern etc. However, we will diverge a bit from the standard clustering algorithms (although we will use one as supporting tool) and try to achieve this through embeddings.   

*What is an embedding*  

</br> 
### The Dataset 

The dataset consists of two main data sources related to the performance telemetry and the virtual hardware of the virtual machines (VMs).

The **performance telemetry** is organized in a python list, containing multiple python dictionaries. Each dictionary accounts for the data of single VM. The key of the dictionary is the respective ID of the VM, and the value is pandas data frame indexed by the timestamp and containing the actual measurements of each feature.  

</br>

Variable Name |Df index| type|unit | Description|
--- | --- |--- | --- |---
ts  |yes|timestamp|time|Time stamp (yyyy-mm-dd HH:MM:SS) of the observation|
cpu_run  |no|numeric|milliseconds|The time the virtual machine is using the CPU|
cpu_ready|no|numeric|milliseconds|The time the virtual machine wants to run a program on the CPU but waits to be scheduled|
mem_active|no|numeric|kiloBytes|The amount of memory that is actively used|
mem_activewrite|no|numeric|kiloBytes|Estimate for the amount of memory actively being written to by the virtual machine.|
net_packetsRx|no|numeric|count|Number of packets received during the interval.|
net_packetsTx|np|numeric|count|Number of packets transmitted during the interval.|

</br> 
The **virtual hardware dataset** is a normal rectangular data frame indexed by the id of the VM. It represents “static” features that account basically for the scale of the system.  
</br>  
  

Variable Name |Df index| type|unit | Description|
--- | --- |--- | --- |---
id  |yes|integer| |Unique identifier of the virtual machine |
memory_mb|no|integer|megabytes|Configured virtual RAM|
num_vcpus|no|integer|count|Number of virtual processor cores|
number_of_nics|no|integer|count|Number of network interface cards|
num_virtual_disks|no|integer|count|Number of the configured hdd|
os_fam|no|categorical|indetity|The operating system of the VM|


The workshop is hoster through google colab  
It requires you to have google accout with ~ 50Mb of available storage 
The notebook can be found at:  
https://drive.google.com/open?id=1mKx2sAdSNuslQtUsRqREsWPiGuBODtEe
