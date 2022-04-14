# spine1-CAS
# Table of Contents

- [Management](#management)
  - [Management Interfaces](#management-interfaces)
  - [Name Servers](#name-servers)
  - [Management API HTTP](#management-api-http)
- [Authentication](#authentication)
  - [Local Users](#local-users)
- [Monitoring](#monitoring)
- [Spanning Tree](#spanning-tree)
  - [Spanning Tree Summary](#spanning-tree-summary)
  - [Spanning Tree Device Configuration](#spanning-tree-device-configuration)
- [Internal VLAN Allocation Policy](#internal-vlan-allocation-policy)
  - [Internal VLAN Allocation Policy Summary](#internal-vlan-allocation-policy-summary)
  - [Internal VLAN Allocation Policy Configuration](#internal-vlan-allocation-policy-configuration)
- [Interfaces](#interfaces)
  - [Ethernet Interfaces](#ethernet-interfaces)
  - [Loopback Interfaces](#loopback-interfaces)
- [Routing](#routing)
  - [Service Routing Protocols Model](#service-routing-protocols-model)
  - [IP Routing](#ip-routing)
  - [IPv6 Routing](#ipv6-routing)
  - [Static Routes](#static-routes)
  - [Router BGP](#router-bgp)
- [BFD](#bfd)
  - [Router BFD](#router-bfd)
- [Multicast](#multicast)
- [Filters](#filters)
  - [Prefix-lists](#prefix-lists)
  - [Route-maps](#route-maps)
- [ACL](#acl)
- [VRF Instances](#vrf-instances)
  - [VRF Instances Summary](#vrf-instances-summary)
  - [VRF Instances Device Configuration](#vrf-instances-device-configuration)
- [Quality Of Service](#quality-of-service)

# Management

## Management Interfaces

### Management Interfaces Summary

#### IPv4

| Management Interface | description | Type | VRF | IP Address | Gateway |
| -------------------- | ----------- | ---- | --- | ---------- | ------- |
| Management1 | oob_management | oob | MGMT | 198.18.107.211/23 | 198.18.106.1 |

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
   ip address 198.18.107.211/23
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

# Spanning Tree

## Spanning Tree Summary

STP mode: **none**

## Spanning Tree Device Configuration

```eos
!
spanning-tree mode none
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

# Interfaces

## Ethernet Interfaces

### Ethernet Interfaces Summary

#### L2

| Interface | Description | Mode | VLANs | Native VLAN | Trunk Group | Channel-Group |
| --------- | ----------- | ---- | ----- | ----------- | ----------- | ------------- |

*Inherited from Port-Channel Interface

#### IPv4

| Interface | Description | Type | Channel Group | IP Address | VRF |  MTU | Shutdown | ACL In | ACL Out |
| --------- | ----------- | -----| ------------- | ---------- | ----| ---- | -------- | ------ | ------- |
| Ethernet1 | P2P_LINK_TO_LEAF1-CAS_Ethernet3 | routed | - | 172.21.211.8/31 | default | 1500 | false | - | - |
| Ethernet2 | P2P_LINK_TO_LEAF2-CAS_Ethernet3 | routed | - | 172.21.211.12/31 | default | 1500 | false | - | - |
| Ethernet3 | P2P_LINK_TO_LEAF3-CAS_Ethernet3 | routed | - | 172.21.211.16/31 | default | 1500 | false | - | - |
| Ethernet4 | P2P_LINK_TO_LEAF4-CAS_Ethernet3 | routed | - | 172.21.211.20/31 | default | 1500 | false | - | - |
| Ethernet5 | P2P_LINK_TO_BORDERLEAF1-CAS_Ethernet3 | routed | - | 172.21.211.0/31 | default | 1500 | false | - | - |
| Ethernet6 | P2P_LINK_TO_BORDERLEAF2-CAS_Ethernet3 | routed | - | 172.21.211.4/31 | default | 1500 | false | - | - |

### Ethernet Interfaces Device Configuration

```eos
!
interface Ethernet1
   description P2P_LINK_TO_LEAF1-CAS_Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 172.21.211.8/31
!
interface Ethernet2
   description P2P_LINK_TO_LEAF2-CAS_Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 172.21.211.12/31
!
interface Ethernet3
   description P2P_LINK_TO_LEAF3-CAS_Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 172.21.211.16/31
!
interface Ethernet4
   description P2P_LINK_TO_LEAF4-CAS_Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 172.21.211.20/31
!
interface Ethernet5
   description P2P_LINK_TO_BORDERLEAF1-CAS_Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 172.21.211.0/31
!
interface Ethernet6
   description P2P_LINK_TO_BORDERLEAF2-CAS_Ethernet3
   no shutdown
   mtu 1500
   no switchport
   ip address 172.21.211.4/31
```

## Loopback Interfaces

### Loopback Interfaces Summary

#### IPv4

| Interface | Description | VRF | IP Address |
| --------- | ----------- | --- | ---------- |
| Loopback0 | EVPN_Overlay_Peering | default | 172.31.210.1/32 |

#### IPv6

| Interface | Description | VRF | IPv6 Address |
| --------- | ----------- | --- | ------------ |
| Loopback0 | EVPN_Overlay_Peering | default | - |


### Loopback Interfaces Device Configuration

```eos
!
interface Loopback0
   description EVPN_Overlay_Peering
   no shutdown
   ip address 172.31.210.1/32
```

# Routing
## Service Routing Protocols Model

Multi agent routing protocol model enabled

```eos
!
service routing protocols model multi-agent
```

## IP Routing

### IP Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | true |
| MGMT | false |

### IP Routing Device Configuration

```eos
!
ip routing
no ip routing vrf MGMT
```
## IPv6 Routing

### IPv6 Routing Summary

| VRF | Routing Enabled |
| --- | --------------- |
| default | false |
| MGMT | false |

## Static Routes

### Static Routes Summary

| VRF | Destination Prefix | Next Hop IP             | Exit interface      | Administrative Distance       | Tag               | Route Name                    | Metric         |
| --- | ------------------ | ----------------------- | ------------------- | ----------------------------- | ----------------- | ----------------------------- | -------------- |
| MGMT  | 0.0.0.0/0 |  198.18.106.1  |  -  |  1  |  -  |  -  |  - |

### Static Routes Device Configuration

```eos
!
ip route vrf MGMT 0.0.0.0/0 198.18.106.1
```

## Router BGP

### Router BGP Summary

| BGP AS | Router ID |
| ------ | --------- |
| 65100|  172.31.210.1 |

| BGP Tuning |
| ---------- |
| maximum-paths 4 ecmp 4 |

### Router BGP Peer Groups

#### EVPN-OVERLAY-PEERS

| Settings | Value |
| -------- | ----- |
| Address Family | evpn |
| Next-hop unchanged | True |
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

### BGP Neighbors

| Neighbor | Remote AS | VRF | Shutdown | Send-community | Maximum-routes | Allowas-in | BFD |
| -------- | --------- | --- | -------- | -------------- | -------------- | ---------- | --- |
| 172.21.211.1 | 65110 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.21.211.5 | 65110 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.21.211.9 | 65111 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.21.211.13 | 65111 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.21.211.17 | 65112 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.21.211.21 | 65112 | default | - | Inherited from peer group IPv4-UNDERLAY-PEERS | Inherited from peer group IPv4-UNDERLAY-PEERS | - | - |
| 172.30.211.3 | 65110 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS |
| 172.30.211.4 | 65110 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS |
| 172.30.211.5 | 65111 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS |
| 172.30.211.6 | 65111 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS |
| 172.30.211.7 | 65112 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS |
| 172.30.211.8 | 65112 | default | - | Inherited from peer group EVPN-OVERLAY-PEERS | Inherited from peer group EVPN-OVERLAY-PEERS | - | Inherited from peer group EVPN-OVERLAY-PEERS |

### Router BGP EVPN Address Family

#### EVPN Peer Groups

| Peer Group | Activate |
| ---------- | -------- |
| EVPN-OVERLAY-PEERS | True |

### Router BGP Device Configuration

```eos
!
router bgp 65100
   router-id 172.31.210.1
   maximum-paths 4 ecmp 4
   neighbor EVPN-OVERLAY-PEERS peer group
   neighbor EVPN-OVERLAY-PEERS next-hop-unchanged
   neighbor EVPN-OVERLAY-PEERS update-source Loopback0
   neighbor EVPN-OVERLAY-PEERS bfd
   neighbor EVPN-OVERLAY-PEERS ebgp-multihop 3
   neighbor EVPN-OVERLAY-PEERS send-community
   neighbor EVPN-OVERLAY-PEERS maximum-routes 0
   neighbor IPv4-UNDERLAY-PEERS peer group
   neighbor IPv4-UNDERLAY-PEERS send-community
   neighbor IPv4-UNDERLAY-PEERS maximum-routes 12000
   neighbor 172.21.211.1 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.21.211.1 remote-as 65110
   neighbor 172.21.211.1 description borderleaf1-CAS_Ethernet3
   neighbor 172.21.211.5 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.21.211.5 remote-as 65110
   neighbor 172.21.211.5 description borderleaf2-CAS_Ethernet3
   neighbor 172.21.211.9 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.21.211.9 remote-as 65111
   neighbor 172.21.211.9 description leaf1-CAS_Ethernet3
   neighbor 172.21.211.13 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.21.211.13 remote-as 65111
   neighbor 172.21.211.13 description leaf2-CAS_Ethernet3
   neighbor 172.21.211.17 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.21.211.17 remote-as 65112
   neighbor 172.21.211.17 description leaf3-CAS_Ethernet3
   neighbor 172.21.211.21 peer group IPv4-UNDERLAY-PEERS
   neighbor 172.21.211.21 remote-as 65112
   neighbor 172.21.211.21 description leaf4-CAS_Ethernet3
   neighbor 172.30.211.3 peer group EVPN-OVERLAY-PEERS
   neighbor 172.30.211.3 remote-as 65110
   neighbor 172.30.211.3 description borderleaf1-CAS
   neighbor 172.30.211.4 peer group EVPN-OVERLAY-PEERS
   neighbor 172.30.211.4 remote-as 65110
   neighbor 172.30.211.4 description borderleaf2-CAS
   neighbor 172.30.211.5 peer group EVPN-OVERLAY-PEERS
   neighbor 172.30.211.5 remote-as 65111
   neighbor 172.30.211.5 description leaf1-CAS
   neighbor 172.30.211.6 peer group EVPN-OVERLAY-PEERS
   neighbor 172.30.211.6 remote-as 65111
   neighbor 172.30.211.6 description leaf2-CAS
   neighbor 172.30.211.7 peer group EVPN-OVERLAY-PEERS
   neighbor 172.30.211.7 remote-as 65112
   neighbor 172.30.211.7 description leaf3-CAS
   neighbor 172.30.211.8 peer group EVPN-OVERLAY-PEERS
   neighbor 172.30.211.8 remote-as 65112
   neighbor 172.30.211.8 description leaf4-CAS
   redistribute connected route-map RM-CONN-2-BGP
   !
   address-family evpn
      neighbor EVPN-OVERLAY-PEERS activate
   !
   address-family ipv4
      no neighbor EVPN-OVERLAY-PEERS activate
      neighbor IPv4-UNDERLAY-PEERS activate
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

# Filters

## Prefix-lists

### Prefix-lists Summary

#### PL-LOOPBACKS-EVPN-OVERLAY

| Sequence | Action |
| -------- | ------ |
| 10 | permit 172.31.210.0/24 eq 32 |

### Prefix-lists Device Configuration

```eos
!
ip prefix-list PL-LOOPBACKS-EVPN-OVERLAY
   seq 10 permit 172.31.210.0/24 eq 32
```

## Route-maps

### Route-maps Summary

#### RM-CONN-2-BGP

| Sequence | Type | Match and/or Set |
| -------- | ---- | ---------------- |
| 10 | permit | match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY |

### Route-maps Device Configuration

```eos
!
route-map RM-CONN-2-BGP permit 10
   match ip address prefix-list PL-LOOPBACKS-EVPN-OVERLAY
```

# ACL

# VRF Instances

## VRF Instances Summary

| VRF Name | IP Routing |
| -------- | ---------- |
| MGMT | disabled |

## VRF Instances Device Configuration

```eos
!
vrf instance MGMT
```

# Quality Of Service
