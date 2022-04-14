# DC

# Table of Contents

- [Fabric Switches and Management IP](#fabric-switches-and-management-ip)
  - [Fabric Switches with inband Management IP](#fabric-switches-with-inband-management-ip)
- [Fabric Topology](#fabric-topology)
- [Fabric IP Allocation](#fabric-ip-allocation)
  - [Fabric Point-To-Point Links](#fabric-point-to-point-links)
  - [Point-To-Point Links Node Allocation](#point-to-point-links-node-allocation)
  - [Loopback Interfaces (BGP EVPN Peering)](#loopback-interfaces-bgp-evpn-peering)
  - [Loopback0 Interfaces Node Allocation](#loopback0-interfaces-node-allocation)
  - [VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)](#vtep-loopback-vxlan-tunnel-source-interfaces-vteps-only)
  - [VTEP Loopback Node allocation](#vtep-loopback-node-allocation)

# Fabric Switches and Management IP

| POD | Type | Node | Management IP | Platform | Provisioned in CloudVision |
| --- | ---- | ---- | ------------- | -------- | -------------------------- |
| DC | l3leaf | borderleaf1-CAS | 198.18.107.213/23 | vEOS-LAB | Provisioned |
| DC | l3leaf | borderleaf1-OI | 198.18.107.223/23 | vEOS-LAB | Provisioned |
| DC | l3leaf | borderleaf2-CAS | 198.18.107.214/23 | vEOS-LAB | Provisioned |
| DC | l3leaf | borderleaf2-OI | 198.18.107.224/23 | vEOS-LAB | Provisioned |
| DC | l3leaf | leaf1-CAS | 198.18.107.215/23 | vEOS-LAB | Provisioned |
| DC | l3leaf | leaf1-OI | 198.18.107.225/23 | vEOS-LAB | Provisioned |
| DC | l3leaf | leaf2-CAS | 198.18.107.216/23 | vEOS-LAB | Provisioned |
| DC | l3leaf | leaf2-OI | 198.18.107.226/23 | vEOS-LAB | Provisioned |
| DC | l3leaf | leaf3-CAS | 198.18.107.217/23 | vEOS-LAB | Provisioned |
| DC | l3leaf | leaf3-OI | 198.18.107.227/23 | vEOS-LAB | Provisioned |
| DC | l3leaf | leaf4-CAS | 198.18.107.218/23 | vEOS-LAB | Provisioned |
| DC | l3leaf | leaf4-OI | 198.18.107.228/23 | vEOS-LAB | Provisioned |
| DC | spine | spine1-CAS | 198.18.107.211/23 | vEOS-LAB | Provisioned |
| DC | spine | spine1-OI | 198.18.107.221/23 | vEOS-LAB | Provisioned |
| DC | spine | spine2-CAS | 198.18.107.212/23 | vEOS-LAB | Provisioned |
| DC | spine | spine2-OI | 198.18.107.222/23 | vEOS-LAB | Provisioned |

> Provision status is based on Ansible inventory declaration and do not represent real status from CloudVision.

## Fabric Switches with inband Management IP
| POD | Type | Node | Management IP | Inband Interface |
| --- | ---- | ---- | ------------- | ---------------- |

# Fabric Topology

| Type | Node | Node Interface | Peer Type | Peer Node | Peer Interface |
| ---- | ---- | -------------- | --------- | ----------| -------------- |
| l3leaf | borderleaf1-CAS | Ethernet1 | mlag_peer | borderleaf2-CAS | Ethernet1 |
| l3leaf | borderleaf1-CAS | Ethernet2 | mlag_peer | borderleaf2-CAS | Ethernet2 |
| l3leaf | borderleaf1-CAS | Ethernet3 | spine | spine1-CAS | Ethernet5 |
| l3leaf | borderleaf1-CAS | Ethernet4 | spine | spine2-CAS | Ethernet5 |
| l3leaf | borderleaf1-CAS | Ethernet5 | l3leaf | borderleaf1-OI | Ethernet5 |
| l3leaf | borderleaf1-OI | Ethernet1 | mlag_peer | borderleaf2-OI | Ethernet1 |
| l3leaf | borderleaf1-OI | Ethernet2 | mlag_peer | borderleaf2-OI | Ethernet2 |
| l3leaf | borderleaf1-OI | Ethernet3 | spine | spine1-OI | Ethernet5 |
| l3leaf | borderleaf1-OI | Ethernet4 | spine | spine2-OI | Ethernet5 |
| l3leaf | borderleaf2-CAS | Ethernet3 | spine | spine1-CAS | Ethernet6 |
| l3leaf | borderleaf2-CAS | Ethernet4 | spine | spine2-CAS | Ethernet6 |
| l3leaf | borderleaf2-CAS | Ethernet5 | l3leaf | borderleaf2-OI | Ethernet5 |
| l3leaf | borderleaf2-OI | Ethernet3 | spine | spine1-OI | Ethernet6 |
| l3leaf | borderleaf2-OI | Ethernet4 | spine | spine2-OI | Ethernet6 |
| l3leaf | leaf1-CAS | Ethernet1 | mlag_peer | leaf2-CAS | Ethernet1 |
| l3leaf | leaf1-CAS | Ethernet2 | mlag_peer | leaf2-CAS | Ethernet2 |
| l3leaf | leaf1-CAS | Ethernet3 | spine | spine1-CAS | Ethernet1 |
| l3leaf | leaf1-CAS | Ethernet4 | spine | spine2-CAS | Ethernet1 |
| l3leaf | leaf1-OI | Ethernet1 | mlag_peer | leaf2-OI | Ethernet1 |
| l3leaf | leaf1-OI | Ethernet2 | mlag_peer | leaf2-OI | Ethernet2 |
| l3leaf | leaf1-OI | Ethernet3 | spine | spine1-OI | Ethernet1 |
| l3leaf | leaf1-OI | Ethernet4 | spine | spine2-OI | Ethernet1 |
| l3leaf | leaf2-CAS | Ethernet3 | spine | spine1-CAS | Ethernet2 |
| l3leaf | leaf2-CAS | Ethernet4 | spine | spine2-CAS | Ethernet2 |
| l3leaf | leaf2-OI | Ethernet3 | spine | spine1-OI | Ethernet2 |
| l3leaf | leaf2-OI | Ethernet4 | spine | spine2-OI | Ethernet2 |
| l3leaf | leaf3-CAS | Ethernet1 | mlag_peer | leaf4-CAS | Ethernet1 |
| l3leaf | leaf3-CAS | Ethernet2 | mlag_peer | leaf4-CAS | Ethernet2 |
| l3leaf | leaf3-CAS | Ethernet3 | spine | spine1-CAS | Ethernet3 |
| l3leaf | leaf3-CAS | Ethernet4 | spine | spine2-CAS | Ethernet3 |
| l3leaf | leaf3-OI | Ethernet1 | mlag_peer | leaf4-OI | Ethernet1 |
| l3leaf | leaf3-OI | Ethernet2 | mlag_peer | leaf4-OI | Ethernet2 |
| l3leaf | leaf3-OI | Ethernet3 | spine | spine1-OI | Ethernet3 |
| l3leaf | leaf3-OI | Ethernet4 | spine | spine2-OI | Ethernet3 |
| l3leaf | leaf4-CAS | Ethernet3 | spine | spine1-CAS | Ethernet4 |
| l3leaf | leaf4-CAS | Ethernet4 | spine | spine2-CAS | Ethernet4 |
| l3leaf | leaf4-OI | Ethernet3 | spine | spine1-OI | Ethernet4 |
| l3leaf | leaf4-OI | Ethernet4 | spine | spine2-OI | Ethernet4 |

# Fabric IP Allocation

## Fabric Point-To-Point Links

| Uplink IPv4 Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ---------------- | ------------------- | ------------------ | ------------------ |
| 172.21.211.0/24 | 256 | 24 | 9.38 % |
| 172.21.221.0/24 | 256 | 24 | 9.38 % |

## Point-To-Point Links Node Allocation

| Node | Node Interface | Node IP Address | Peer Node | Peer Interface | Peer IP Address |
| ---- | -------------- | --------------- | --------- | -------------- | --------------- |
| borderleaf1-CAS | Ethernet3 | 172.21.211.1/31 | spine1-CAS | Ethernet5 | 172.21.211.0/31 |
| borderleaf1-CAS | Ethernet4 | 172.21.211.3/31 | spine2-CAS | Ethernet5 | 172.21.211.2/31 |
| borderleaf1-CAS | Ethernet5 | 172.20.100.0/31 | borderleaf1-OI | Ethernet5 | 172.20.100.1/31 |
| borderleaf1-OI | Ethernet3 | 172.21.221.1/31 | spine1-OI | Ethernet5 | 172.21.221.0/31 |
| borderleaf1-OI | Ethernet4 | 172.21.221.3/31 | spine2-OI | Ethernet5 | 172.21.221.2/31 |
| borderleaf2-CAS | Ethernet3 | 172.21.211.5/31 | spine1-CAS | Ethernet6 | 172.21.211.4/31 |
| borderleaf2-CAS | Ethernet4 | 172.21.211.7/31 | spine2-CAS | Ethernet6 | 172.21.211.6/31 |
| borderleaf2-CAS | Ethernet5 | 172.20.100.2/31 | borderleaf2-OI | Ethernet5 | 172.20.100.3/31 |
| borderleaf2-OI | Ethernet3 | 172.21.221.5/31 | spine1-OI | Ethernet6 | 172.21.221.4/31 |
| borderleaf2-OI | Ethernet4 | 172.21.221.7/31 | spine2-OI | Ethernet6 | 172.21.221.6/31 |
| leaf1-CAS | Ethernet3 | 172.21.211.9/31 | spine1-CAS | Ethernet1 | 172.21.211.8/31 |
| leaf1-CAS | Ethernet4 | 172.21.211.11/31 | spine2-CAS | Ethernet1 | 172.21.211.10/31 |
| leaf1-OI | Ethernet3 | 172.21.221.9/31 | spine1-OI | Ethernet1 | 172.21.221.8/31 |
| leaf1-OI | Ethernet4 | 172.21.221.11/31 | spine2-OI | Ethernet1 | 172.21.221.10/31 |
| leaf2-CAS | Ethernet3 | 172.21.211.13/31 | spine1-CAS | Ethernet2 | 172.21.211.12/31 |
| leaf2-CAS | Ethernet4 | 172.21.211.15/31 | spine2-CAS | Ethernet2 | 172.21.211.14/31 |
| leaf2-OI | Ethernet3 | 172.21.221.13/31 | spine1-OI | Ethernet2 | 172.21.221.12/31 |
| leaf2-OI | Ethernet4 | 172.21.221.15/31 | spine2-OI | Ethernet2 | 172.21.221.14/31 |
| leaf3-CAS | Ethernet3 | 172.21.211.17/31 | spine1-CAS | Ethernet3 | 172.21.211.16/31 |
| leaf3-CAS | Ethernet4 | 172.21.211.19/31 | spine2-CAS | Ethernet3 | 172.21.211.18/31 |
| leaf3-OI | Ethernet3 | 172.21.221.17/31 | spine1-OI | Ethernet3 | 172.21.221.16/31 |
| leaf3-OI | Ethernet4 | 172.21.221.19/31 | spine2-OI | Ethernet3 | 172.21.221.18/31 |
| leaf4-CAS | Ethernet3 | 172.21.211.21/31 | spine1-CAS | Ethernet4 | 172.21.211.20/31 |
| leaf4-CAS | Ethernet4 | 172.21.211.23/31 | spine2-CAS | Ethernet4 | 172.21.211.22/31 |
| leaf4-OI | Ethernet3 | 172.21.221.21/31 | spine1-OI | Ethernet4 | 172.21.221.20/31 |
| leaf4-OI | Ethernet4 | 172.21.221.23/31 | spine2-OI | Ethernet4 | 172.21.221.22/31 |

## Loopback Interfaces (BGP EVPN Peering)

| Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| ------------- | ------------------- | ------------------ | ------------------ |
| 172.30.211.0/24 | 256 | 6 | 2.35 % |
| 172.30.221.0/24 | 256 | 6 | 2.35 % |
| 172.31.210.0/24 | 256 | 2 | 0.79 % |
| 172.31.220.0/24 | 256 | 2 | 0.79 % |

## Loopback0 Interfaces Node Allocation

| POD | Node | Loopback0 |
| --- | ---- | --------- |
| DC | borderleaf1-CAS | 172.30.211.3/32 |
| DC | borderleaf1-OI | 172.30.221.3/32 |
| DC | borderleaf2-CAS | 172.30.211.4/32 |
| DC | borderleaf2-OI | 172.30.221.4/32 |
| DC | leaf1-CAS | 172.30.211.5/32 |
| DC | leaf1-OI | 172.30.221.5/32 |
| DC | leaf2-CAS | 172.30.211.6/32 |
| DC | leaf2-OI | 172.30.221.6/32 |
| DC | leaf3-CAS | 172.30.211.7/32 |
| DC | leaf3-OI | 172.30.221.7/32 |
| DC | leaf4-CAS | 172.30.211.8/32 |
| DC | leaf4-OI | 172.30.221.8/32 |
| DC | spine1-CAS | 172.31.210.1/32 |
| DC | spine1-OI | 172.31.220.1/32 |
| DC | spine2-CAS | 172.31.210.2/32 |
| DC | spine2-OI | 172.31.220.2/32 |

## VTEP Loopback VXLAN Tunnel Source Interfaces (VTEPs Only)

| VTEP Loopback Pool | Available Addresses | Assigned addresses | Assigned Address % |
| --------------------- | ------------------- | ------------------ | ------------------ |
| 172.31.211.0/24 | 256 | 6 | 2.35 % |
| 172.31.221.0/24 | 256 | 6 | 2.35 % |

## VTEP Loopback Node allocation

| POD | Node | Loopback1 |
| --- | ---- | --------- |
| DC | borderleaf1-CAS | 172.31.211.3/32 |
| DC | borderleaf1-OI | 172.31.221.3/32 |
| DC | borderleaf2-CAS | 172.31.211.3/32 |
| DC | borderleaf2-OI | 172.31.221.3/32 |
| DC | leaf1-CAS | 172.31.211.5/32 |
| DC | leaf1-OI | 172.31.221.5/32 |
| DC | leaf2-CAS | 172.31.211.5/32 |
| DC | leaf2-OI | 172.31.221.5/32 |
| DC | leaf3-CAS | 172.31.211.7/32 |
| DC | leaf3-OI | 172.31.221.7/32 |
| DC | leaf4-CAS | 172.31.211.7/32 |
| DC | leaf4-OI | 172.31.221.7/32 |
