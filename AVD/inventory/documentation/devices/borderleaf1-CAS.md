# borderleaf1-CAS
# Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [Name Servers](#name-servers)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
- [Monitoring](#monitoring)
- [MLAG](#mlag)
  - [MLAG Summary](#mlag-summary)
  - [MLAG Device Configuration](#mlag-device-configuration)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Configuration](#internal-vlan-allocation-policy-configuration)
- [VLANs](#vlans)
  - [VLANs Summary](#vlans-summary)
  - [VLANs Device Configuration](#vlans-device-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Port-Channel Interfaces](#port-channel-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
  - [VLAN Interfaces](#vlan-interfaces)
  - [VXLAN Interface](#vxlan-interface)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [Virtual Router MAC Address](#virtual-router-mac-address)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Multicast](#multicast)
  - [IP IGMP Snooping](#ip-igmp-snooping)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
- [ACL](#acl)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [Virtual Source NAT](#virtual-source-nat)
  - [Virtual Source NAT Summary](#virtual-source-nat-summary)
  - [Virtual Source NAT Configuration](#virtual-source-nat-configuration)
- [Quality Of Service](#quality-of-service)

# Management

## Management Interfaces

### Management Interfaces Summary

#### IPv4

| Management Interface | description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | oob_management | oob | MGMT | 198.18.107.213/23 | 198.18.106.1 |

#### IPv6

| Management Interface | description | Type | VRF | IPv6 Address | IPv6 Gateway |
| -------------------- | ----------- | ---- | --- | ------------ | ------------ |
| Management1 | oob_management | oob | MGMT | -  | - |

### Management Interfaces Device Configuration

```eos
!
interface Management1
   description oob_management
   no shutdown
   vrf MGMT
   ip address 198.18.107.213/23
```

## Name Servers

### Name Servers Summary

| Name Server | Source VRF |
| ----------- | ---------- |
| 208.67.222.222 | MGMT |
| 8.8.8.8 | MGMT |

### Name Servers Device Configuration

```eos
ip name-server vrf MGMT 8.8.8.8
ip name-server vrf MGMT 208.67.222.222
```

## Management API HTTP

### Management API HTTP Summary

| HTTP | HTTPS |
| ---- | ----- |
| False | True |

### Management API VRF Access

| VRF Name | IPv4 ACL | IPv6 ACL |
| -------- | -------- | -------- |
| MGMT | - | - |

### Management API HTTP Configuration

```eos
!
management api http-commands
   protocol https
   no shutdown
   !
   vrf MGMT
      no shutdown
```

# Authentication

## Local Users

### Local Users Summary

| User | Privilege | Role |
| ---- | --------- | ---- |
| ansible | 15 | network-admin |
| netadmin | 15 | network-admin |

### Local Users Device Configuration

```eos
!
username ansible privilege 15 role network-admin secret sha512 $6$k2QzB8961/dFJf35$HLuhZBTypOM05zmGx99BAHI0.Zok8GUVm303zaZTJhQmp.cKq84un1e.cqztvC8ZFqRN6bCc.GkOknMBurXki.
username netadmin privilege 15 role network-admin secret sha512 $6$cK1bIDtMtCcnZC.1$/WgQmDoQ4pv4et2vYjX8M65SW667tVQreVBItTinbqOLP4Ef41bSt8rKLoLJMvwYLSw7gVJJMxUBdL1jagQ.9.
```

# Monitoring

# MLAG

## MLAG Summary

| Domain-id | Local-interface | Peer-address | Peer-link |
| --------- | --------------- | ------------ | --------- |
| CAS_BORDERLEAFS | Vlan4094 | 10.255.252.1 | Port-Channel1 |

Dual primary detection is disabled.

## MLAG Device Configuration

```eos
!
mlag configuration
   domain-id CAS_BORDERLEAFS
   local-interface Vlan4094
   peer-address 10.255.252.1
   peer-link Port-Channel1
   reload-delay mlag 300
   reload-delay non-mlag 330
```

# Spanning Tree

## Spanning Tree Summary

STP mode: **mstp**

### MSTP Instance and Priority

| Instance(s) | Priority |
| -------- | -------- |
| 0 | 4096 |

### Global Spanning-Tree Settings

- Spanning Tree disabled for VLANs: **4093-4094**

## Spanning Tree Device Configuration

```eos
!
spanning-tree mode mstp
no spanning-tree vlan-id 4093-4094
spanning-tree mst 0 priority 4096
```

# Internal VLAN Allocation Policy

## Internal VLAN Allocation Policy Summary

| Policy Allocation | Range Beginning | Range Ending |
| ------------------| --------------- | ------------ |
| ascending | 1006 | 1199 |

## Internal VLAN Allocation Policy Configuration

```eos
!
vlan internal order ascending range 1006 1199
```

# VLANs

## VLANs Summary

| VLAN ID | Name | Trunk Groups |
| ------- | ---- | ------------ |
| 100 | FW_CLUSTER | - |
| 101 | FW_INTERNA | - |
| 102 | FW_SERVICO | - |
| 1110 | FrontEnd_OP_Zone_1 | - |
| 1111 | FrontEnd_OP_Zone_2 | - |
| 3110 | MLAG_iBGP_FW_Outside | LEAF_PEER_L3 |
| 4093 | LEAF_PEER_L3 | LEAF_PEER_L3 |
| 4094 | MLAG_PEER | MLAG |

## VLANs Device Configuration

```eos
!
vlan 100
   name FW_CLUSTER
!
vlan 101
   name FW_INTERNA
!
vlan 102
   name FW_SERVICO
!
vlan 1110
   name FrontEnd_OP_Zone_1
!
vlan 1111
   name FrontEnd_OP_Zone_2
!
vlan 3110
   name MLAG_iBGP_FW_Outside
   trunk group LEAF_PEER_L3
!
vlan 4093
   name LEAF_PEER_L3
   trunk group LEAF_PEER_L3
!
vlan 4094
   name MLAG_PEER
   trunk group MLAG
```

# Interfaces

## Ethernet Interfaces

### Ethernet Interfaces Summary

#### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |
| Ethernet1 | MLAG_PEER_borderleaf2-CAS_Ethernet1 | *trunk | *2-4094 | *- | *['LEAF_PEER_L3', 'MLAG'] | 1 |
| Ethernet2 | MLAG_PEER_borderleaf2-CAS_Ethernet2 | *trunk | *2-4094 | *- | *['LEAF_PEER_L3', 'MLAG'] | 1 |
| Ethernet6 |  FW_CLIENTE_Eth0 | trunk | 101,102,1110 | - | - | - |

*Inherited from Port-Channel Interface

#### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet3 | P2P_LINK_TO_SPINE1-CAS_Ethernet5 | routed | - | 172.21.211.1/31 | default | 1500 | false | - | - |
| Ethernet4 | P2P_LINK_TO_SPINE2-CAS_Ethernet5 | routed | - | 172.21.211.3/31 | default | 1500 | false | - | - |
| Ethernet5 | P2P_LINK_TO_borderleaf1-OI_Ethernet5 | routed | - | 172.20.100.0/31 | default | 1500 | false | - | - |

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description MLAG_PEER_borderleaf2-CAS_Ethernet1
   no shutdown
   channel-group 1 mode active
!
interface Ethernet2
   description MLAG_PEER_borderleaf2-CAS_Ethernet2
   no shutdown
   channel-group 1 mode active
!
interface Ethernet3
   description P2P_LINK_TO_SPINE1-CAS_Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 172.21.211.1/31
!
interface Ethernet4
   description P2P_LINK_TO_SPINE2-CAS_Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 172.21.211.3/31
!
interface Ethernet5
   description P2P_LINK_TO_borderleaf1-OI_Ethernet5
   no shutdown
   mtu 1500
   no switchport
   ip address 172.20.100.0/31
!
interface Ethernet6
   description FW_CLIENTE_Eth0
   no shutdown
   switchport
   switchport trunk allowed vlan 101,102,1110
   switchport mode trunk
```

## Port-Channel Interfaces

### Port-Channel Interfaces Summary

#### L2

| Interface | Description | Type | Mode | VLANs | Native VLAN | Trunk Group | LACP Fallback Timeout | LACP Fallback Mode | MLAG ID | EVPN ESI |
| --------- | ----------- | ---- | ---- | ----- | ----------- | ------------| --------------------- | ------------------ | ------- | -------- |
| Port-Channel1 | MLAG_PEER_borderleaf2-CAS_Po1 | switched | trunk | 2-4094 | - | ['LEAF_PEER_L3', 'MLAG'] | - | - | - | - |

### Port-Channel Interfaces Device Configuration

```eos
!
interface Port-Channel1
   description MLAG_PEER_borderleaf2-CAS_Po1
   no shutdown
   switchport
   switchport trunk allowed vlan 2-4094
   switchport mode trunk
   switchport trunk group LEAF_PEER_L3
   switchport trunk group MLAG
```

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | EVPN_Overlay_Peering | default | 172.30.211.3/32 |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | 172.31.211.3/32 |
| Loopback100 | FW_Outside_VTEP_DIAGNOSTICS | FW_Outside | 10.255.1.3/32 |

#### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | EVPN_Overlay_Peering | default | - |
| Loopback1 | VTEP_VXLAN_Tunnel_Source | default | - |
| Loopback100 | FW_Outside_VTEP_DIAGNOSTICS | FW_Outside | - |


### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description EVPN_Overlay_Peering
   no shutdown
   ip address 172.30.211.3/32
!
interface Loopback1
   description VTEP_VXLAN_Tunnel_Source
   no shutdown
   ip address 172.31.211.3/32
!
interface Loopback100
   description FW_Outside_VTEP_DIAGNOSTICS
   no shutdown
   vrf FW_Outside
   ip address 10.255.1.3/32
```

## VLAN Interfaces

### VLAN Interfaces Summary

| Interface | Description | VRF |  MTU | Shutdown |
| --------- | ----------- | --- | ---- | -------- |
| Vlan1110 |  FrontEnd_OP_Zone_1  |  FW_Outside  |  -  |  false  |
| Vlan1111 |  FrontEnd_OP_Zone_2  |  FW_Outside  |  -  |  false  |
| Vlan3110 |  MLAG_PEER_L3_iBGP: vrf FW_Outside  |  FW_Outside  |  1500  |  false  |
| Vlan4093 |  MLAG_PEER_L3_PEERING  |  default  |  1500  |  false  |
| Vlan4094 |  MLAG_PEER  |  default  |  1500  |  false  |

#### IPv4

| Interface | VRF | IP Address | IP Address Virtual | IP Router Virtual Address | VRRP | ACL In | ACL Out |
| --------- | --- | ---------- | ------------------ | ------------------------- | ---- | ------ | ------- |
| Vlan1110 |  FW_Outside  |  -  |  10.1.110.1/24  |  -  |  -  |  -  |  -  |
| Vlan1111 |  FW_Outside  |  -  |  10.1.111.1/24  |  -  |  -  |  -  |  -  |
| Vlan3110 |  FW_Outside  |  10.255.251.0/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan4093 |  default  |  10.255.251.0/31  |  -  |  -  |  -  |  -  |  -  |
| Vlan4094 |  default  |  10.255.252.0/31  |  -  |  -  |  -  |  -  |  -  |


### VLAN Interfaces Device Configuration

```eos
!
interface Vlan1110
   description FrontEnd_OP_Zone_1
   no shutdown
   vrf FW_Outside
   ip address virtual 10.1.110.1/24
!
interface Vlan1111
   description FrontEnd_OP_Zone_2
   no shutdown
   vrf FW_Outside
   ip address virtual 10.1.111.1/24
!
interface Vlan3110
   description MLAG_PEER_L3_iBGP: vrf FW_Outside
   no shutdown
   mtu 1500
   vrf FW_Outside
   ip address 10.255.251.0/31
!
interface Vlan4093
   description MLAG_PEER_L3_PEERING
   no shutdown
   mtu 1500
   ip address 10.255.251.0/31
!
interface Vlan4094
   description MLAG_PEER
   no shutdown
   mtu 1500
   no autostate
   ip address 10.255.252.0/31
```

## VXLAN Interface

### VXLAN Interface Summary

| Setting | Value |
| ------- | ----- |
| Source Interface | Loopback1 |
| UDP port | 4789 |
| EVPN MLAG Shared Router MAC | mlag-system-id |

#### VLAN to VNI, Flood List and Multicast Group Mappings

| VLAN | VNI | Flood List | Multicast Group |
| ---- | --- | ---------- | --------------- |
| 100 | 55100 | - | - |
| 101 | 55101 | - | - |
| 102 | 55102 | - | - |
| 1110 | 50110 | - | - |
| 1111 | 50111 | - | - |

#### VRF to VNI and Multicast Group Mappings

| VRF | VNI | Multicast Group |
| ---- | --- | --------------- |
| FW_Outside | 111 | - |

### VXLAN Interface Device Configuration

```eos
!
interface Vxlan1
   description borderleaf1-CAS_VTEP
   vxlan source-interface Loopback1
   vxlan virtual-router encapsulation mac-address mlag-system-id
   vxlan udp-port 4789
   vxlan vlan 100 vni 55100
   vxlan vlan 101 vni 55101
   vxlan vlan 102 vni 55102
   vxlan vlan 1110 vni 50110
   vxlan vlan 1111 vni 50111
   vxlan vrf FW_Outside vni 111
```

# Routing
## Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

## Virtual Router MAC Address

### Virtual Router MAC Address Summary

#### Virtual Router MAC Address: 00:1c:73:00:dc:01

### Virtual Router MAC Address Configuration

```eos
!
ip virtual-router mac-address 00:1c:73:00:dc:01
```

## IP Routing

### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | true |
| FW_Outside | true |
| MGMT | false |

### IP Routing Device Configuration

```eos
!
ip routing
ip routing vrf FW_Outside
no ip routing vrf MGMT
```
## IPv6 Routing

### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | false |
| FW_Outside | false |
| MGMT | false |

## Static Routes

### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP             | Exit interface      | Administrative Distance       | Tag               | Route Name                    | Metric         |
| --- | ------------------ | ----------------------- | ------------------- | ----------------------------- | ----------------- | ----------------------------- | -------------- |
| MGMT  | 0.0.0.0/0 |  198.18.106.1  |  -  |  1  |  -  |  -  |  - |
| FW_Outside  | 0.0.0.0/0 |  10.1.110.254  |  -  |  1  |  -  |  FW_CLUSTER  |  - |

### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 198.18.106.1
ip route vrf FW_Outside 0.0.0.0/0 10.1.110.254 name FW_CLUSTER
```

## Router BGP

### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65110|  172.30.211.3 |

| BGP Tuning |
| ---------- |
| maximum-paths 4 ecmp 4 |

### Router BGP Peer Groups

#### EVPN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| Source | Loopback0 |
| BFD | True |
| Ebgp multihop | 3 |
| Send community | all |
| Maximum routes | 0 (no limit) |

#### IPv4-UNDERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Send community | all |
| Maximum routes | 12000 |

#### MLAG-IPv4-UNDERLAY-PEER

| Settings | Value |
| -------- | ----- |
| Address Family | ipv4 |
| Remote AS | 65110 |
| Next-hop self | True |
| Send community | all |
| Maximum routes | 12000 |

### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- |
| 10.255.251.1 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | default | - | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | - | - |
| 172.20.100.1 | 65210 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.21.211.0 | 65100 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.21.211.2 | 65100 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.31.210.1 | 65100 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS |
| 172.31.210.2 | 65100 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS |
| 10.255.251.1 | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | FW_Outside | - | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | Inherited from peer group MLAG-IPv4-UNDERLAY-PEER | - | - |

### Router BGP EVPN Address Family

#### EVPN Peer Groups

| Peer Group | Activate |
| ---------- | -------- |
| EVPN-OVERLAY-PEERS | True |

### Router BGP VLANs

| VLAN | Route-Distinguisher | Both Route-Target | Import Route Target | Export Route-Target | Redistribute |
| ---- | ------------------- | ----------------- | ------------------- | ------------------- | ------------ |
| 100 | 172.30.211.3:55100 | 55100:55100 | - | - | learned |
| 101 | 172.30.211.3:55101 | 55101:55101 | - | - | learned |
| 102 | 172.30.211.3:55102 | 55102:55102 | - | - | learned |
| 1110 | 172.30.211.3:50110 | 50110:50110 | - | - | learned |
| 1111 | 172.30.211.3:50111 | 50111:50111 | - | - | learned |

### Router BGP VRFs

| VRF | Route-Distinguisher | Redistribute |
| --- | ------------------- | ------------ |
| FW_Outside | 172.30.211.3:111 | connected<br>static |

### Router BGP Device Configuration

```eos
!
router bgp 65110
   router-id 172.30.211.3
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor MLAG-IPv4-UNDERLAY-PEER peer group
   neighbor MLAG-IPv4-UNDERLAY-PEER remote-as 65110
   neighbor MLAG-IPv4-UNDERLAY-PEER next-hop-self
   neighbor MLAG-IPv4-UNDERLAY-PEER send-community
   neighbor MLAG-IPv4-UNDERLAY-PEER maximum-routes 12000
   neighbor MLAG-IPv4-UNDERLAY-PEER route-map RM-MLAG-PEER-IN in
   neighbor 10.255.251.1 peer group MLAG-IPv4-UNDERLAY-PEER
   neighbor 10.255.251.1 description borderleaf2-CAS
   neighbor 172.20.100.1 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.20.100.1 remote-as 65210
   neighbor 172.20.100.1 description borderleaf1-OI
   neighbor 172.21.211.0 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.21.211.0 remote-as 65100
   neighbor 172.21.211.0 description spine1-CAS_Ethernet5
   neighbor 172.21.211.2 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.21.211.2 remote-as 65100
   neighbor 172.21.211.2 description spine2-CAS_Ethernet5
   neighbor 172.31.210.1 peer group EVPN-OVERLAY-PEERS
   neighbor 172.31.210.1 remote-as 65100
   neighbor 172.31.210.1 description spine1-CAS
   neighbor 172.31.210.2 peer group EVPN-OVERLAY-PEERS
   neighbor 172.31.210.2 remote-as 65100
   neighbor 172.31.210.2 description spine2-CAS
   redistribute connected route-map RM-CONN-2-BGP
   !
   vlan 100
      rd 172.30.211.3:55100
      route-target both 55100:55100
      redistribute learned
   !
   vlan 101
      rd 172.30.211.3:55101
      route-target both 55101:55101
      redistribute learned
   !
   vlan 102
      rd 172.30.211.3:55102
      route-target both 55102:55102
      redistribute learned
   !
   vlan 1110
      rd 172.30.211.3:50110
      route-target both 50110:50110
      redistribute learned
   !
   vlan 1111
      rd 172.30.211.3:50111
      route-target both 50111:50111
      redistribute learned
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
      neighbor MLAG-IPv4-UNDERLAY-PEER activate
   !
   vrf FW_Outside
      rd 172.30.211.3:111
      route-target import evpn 111:111
      route-target export evpn 111:111
      router-id 172.30.211.3
      neighbor 10.255.251.1 peer group MLAG-IPv4-UNDERLAY-PEER
      redistribute connected
      redistribute static
```

# BFD

## Router BFD

### Router BFD Multihop Summary

| Interval | Minimum RX | Multiplier |
| -------- | ---------- | ---------- |
| 1200 | 1200 | 3 |

### Router BFD Device Configuration

```eos
!
router bfd
   multihop interval 1200 min-rx 1200 multiplier 3
```

# Multicast

## IP IGMP Snooping

### IP IGMP Snooping Summary

| IGMP Snooping | Fast Leave | Interface Restart Query | Proxy | Restart Query Interval | Robustness Variable |
| ------------- | ---------- | ----------------------- | ----- | ---------------------- | ------------------- |
| Enabled | - | - | - | - | - |

### IP IGMP Snooping Device Configuration

```eos
```

# Filters

## Prefix-lists

### Prefix-lists Summary

#### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 172.30.211.0/24 eq 32 |
| 20 | permit 172.31.211.0/24 eq 32 |

### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 172.30.211.0/24 eq 32
   seq 20 permit 172.31.211.0/24 eq 32
```

## Route-maps

### Route-maps Summary

#### RM-CONN-2-BGP

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY |

#### RM-MLAG-PEER-IN

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | set origin incomplete |

### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
!
route-map RM-MLAG-PEER-IN permit 10
   description Make routes learned over MLAG Peer-link less preferred on spines to ensure optimal routing
   set origin incomplete
```

# ACL

# VRF Instances

## VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| FW_Outside | enabled |
| MGMT | disabled |

## VRF Instances Device Configuration

```eos
!
vrf instance FW_Outside
!
vrf instance MGMT
```

# Virtual Source NAT

## Virtual Source NAT Summary

| Source NAT VRF | Source NAT IP Address |
| -------------- | --------------------- |
| FW_Outside | 10.255.1.3 |

## Virtual Source NAT Configuration

```eos
!
ip address virtual source-nat vrf FW_Outside address 10.255.1.3
```

# Quality Of Service
