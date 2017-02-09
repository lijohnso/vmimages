# OpenStack Cloud Image of VPP SNAT and TREX

## Overview
This repository contains two VM images which have the open sourced application VPP and TREX installed. The VM images are used for test purpose.
The author just installed the applications enabled the applications to start with system boots. Other user could use these two images for their
own tests.

## VPP Introduction
VPP (The open source version of Cisco's Vector Packet Processing technolog, please refer@https://wiki.fd.io/view/VPP/What_is_VPP%3F) is an open
sourced project for packet processing in userspace, it supports most of the TCP/IP features. 
The VPP SNAT is an implementation of NAT44. It is a plugin and is meant to replace the VCGN component. The target use case is a general IPv4 CPE
NAT, a CGN and to act as a NAT44 in a Openstack deployment (from the wiki page: https://wiki.fd.io/view/VPP/SNAT). The VPP SNAT plugin supports
both stateful and stateless NAT, it's quite perfect sample application for the NFV (Network Function Virtualization) environment.

## TREX Introduction
TRex is an open source, low cost, stateful traffic generator fuelled by DPDK(From the wiki page: https://trex-tgn.cisco.com). Since it's open
souced software and could archive quite performance with strong features. It's quite useful tools for network developers and companies.

## How to use
The VM images are from the cloud image of Ubuntu Xenial release, the author changed the root's password to 123456 for easily login from the VNC
window once the system boots up. The VPP or TREX will startup with the system boots. No additional commands or scripts are required to run the
the application. If the user need to do some changes of application, please try to login from the VNC with the root account.

The TREX will try to generte stateful flows from 192.168.50.46 to 10.10.23.46 and the VPP SNAT will try to NAT the flows from local 192.168.50.76
to remote 10.10.23.45. 

Since the VPP and TREX are DPDK-based application, so CPU arch is required for the system, normal QEMU virtual CPU doesn’t support the special
instruction set like SSE4.2, assign CPU model should be done while booting the VM. Otherwise the application might not work as expected.

1.  VPP SNAT
For the VPP SNAT application, the VM requires 1 NIC. To add more rules, please refer to the wiki https://wiki.fd.io/view/VPP/SNAT. 
To stop the application, please run the command:
$ systemctl stop vpp-snat

2.	TREX Packet Generator
For the TREX packet generator, the VM requires at least 4 CPUs, 2GB + of RAM memory, 2 NICs. Once the system boots up, the TREX packet generator is
already running in background, to check the console of TREX application, please use the following command:
$ screen -r trex
To stop the application, please run the command:
$ systemctl stop trex

## Known issues
This is the 1st release, no known issue at the moment, if you have any question, please contact the author.
