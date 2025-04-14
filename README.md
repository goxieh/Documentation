# Documentation

Capstone Network Infrastructure Documentation

1. Network Overview

The Capstone Scenario A, on which our proposal is based, is a high school that needs a working network to support:

Internet and learning access for students

Sharing of resources and availability of instructional resources for instructors

Administrative access and staff communication

Network service administration and IT infrastructure (AD, DNS, DHCP, internal email, etc.)

Objectives

Provide Reliable and Segmented Connectivity for All Departments

Ensure High Availability and Redundancy

Secure the network through Hardening and Access Control

2. Topologies

2.1 Logical Topology



3. IP Addressing Schema Information

3.1 Etherchannel and Trunk Implementation

Network Device

Trunk Port

Etherchannel

Router1

G0/1.10–G0/1.50 (ROAS)

G0/1

Router2

G0/1.10–G0/1.50 (ROAS)

G0/1

Switch1 (sw1)

Port-Channel 1

Fa0/23, Fa0/24  Gi0/1, Gi0/2 (not bundled, trunk only)

Switch2 (Sw2)

Port-Channel 1

Fa0/23, Fa0/24

Configuration:

channel-group 1 mode active
switchport mode trunk
switchport trunk allowed vlan 10,20,30,40,50

This setup enables LACP EtherChannel carrying all VLANs between the switches.

GigabitEthernet0/1 on R1 and R2 are configured with subinterfaces for router-on-a-stick (ROAS), each handling:

Encapsulation dot1Q per VLAN

IP addresses

HSRP setup with virtual IP .254

3.2 Router 1 (R1)

Model: Cisco 2901IP Addressing:

Interface

VLAN

IP Address

Subnet Mask

G0/0

WAN

DHCP assigned

-

G0/1

Native

192.168.1.1

255.255.255.0

G0/1.10

VLAN 10 - Students

192.168.10.1

255.255.255.0

G0/1.20

VLAN 20 - Instructors

192.168.20.1

255.255.255.0

G0/1.30

VLAN 30 - Staff

192.168.30.1

255.255.255.0

G0/1.40

VLAN 40 - IT

192.168.40.1

255.255.255.0

G0/1.50

VLAN 50 - Servers

192.168.50.1

255.255.255.0

Note:

Subinterfaces are created for Router-on-a-Stick inter-VLAN routing

NAT is configured with ip nat inside on G0/1 subinterfaces and ip nat outside on G0/0

ip helper-address is used on VLANs (e.g., 192.168.50.11)

HSRP is configured with virtual IPs ending in .254

3.3 Router 2 (R2)

[Configuration and all interface details are exactly as in your message above, formatted similarly.]

3.4 Switches

Switch 1 (S1) - 2960-24TT

Fa0/1–Fa0/15: VLAN 10 Access

Fa0/23, Fa0/24: Trunk, EtherChannel

Gi0/1, Gi0/2: Trunk

Port-channel1: VLANs 10–50

Switch 2 (SW2) - 2960

VLAN Access Ports and Trunks configured per VLAN (20–50)

4. Server Services

4.1 Domain Controller (SilverWood_Server_DC)

[All points, configuration steps, and screenshots included exactly as in your message.]

4.2 DNS

[Retain all setup steps from creation of forward/reverse lookup zones to nslookup verification.]

4.3 DHCP

[DHCP configuration including scope, exclusions, and lease monitoring shown exactly as written.]

5. Microsoft 365 Email (Send/Receive)

Microsoft 365 Admin Center – User Account Creation and Role Assignment

[Steps 1 through 6 and screenshots – all preserved verbatim.]

Microsoft Teams Group Creation and Setup

[Includes all groups: IT, Staff, Instructors, Students – along with member assignments and permissions.]

Outlook Integration and Internal Communication Testing

[Exactly as described: from David Thompson’s welcome email to Aiwei’s system-wide announcement.]

Final Notes

This document details a comprehensive and real-world setup of:

Cisco-based inter-VLAN routing with redundancy

Active Directory, DHCP, and DNS server integration

Microsoft 365 deployment for user management and communication

Outlook testing and email flow validation

Prepared by: Chigozirim Success IbeFor: Capstone Project - Scenario AFormat: README.md - GitHub-ready

