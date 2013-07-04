actaeon
=======

What is actaeon?
----------------
Actaeon is a tool to perform memory forensics of virtualization environments. 
Starting from a physical memory dump, Actaeon can achieve three important goals: 
1) locate any Hypervisor (virtual machine monitor) that uses the Intel VT-x technology
2) detect and analyze nested virtualization and show the relationships among different hypervisors running on the same machine
3) provide a transparent mechanism to recognize and support the address space of the virtual machines.

Actaeon consists of three components:

- hyperls: a Volatility plugin to list the hypervisors in a memory dump and print several info about them.
- A patch to Volatility to allow other plugins and commands to be applied to each guest operating system.
- A VMCS layout dumper, based on the HyperDbg code

Actaeon adopts a hypervisor-agnostic approach, based on locating the VMCS data structure in memory. Thus, it should be able to detect any hypervisor (benign or malicious) that uses this technology. So far, we successfully tested it with KVM (kernel 3.6.0), Xen (4.2.0), VMware Workstation (9.0.1), VirtualBox (4.2.6) and the last version of HyperDbg - including different nested combinations (e.g., KVM under XEN, or VirtualBox under VMWare). Our tests were limited to 32bit Operating Systems (tests with 64bits and Microsoft Hyper-V are on the way).

Actaeon needs to know the offsets of certain fields inside the VMCS. At the moment, our distribution contains three Intel microarchitectures (Sandy Bridge, Penryn and Westmere) and a number of custom VMCS used to support nested hypervisors (Xen, KVM, and VMWare workstation). 
If you have a processor with another microarchitecture please help us by running our VMCS offset dumper and sending back to us its output.
