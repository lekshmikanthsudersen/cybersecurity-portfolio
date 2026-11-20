# Private virtual lab setup

## Objective

Create a controlled environment for service discovery and verify its network boundary before scanning.

## Environment and tools

VMware Workstation Pro 25H2 hosted Kali Linux 2026.3 at `192.168.77.10/24` and an owned Metasploitable 2 target at `192.168.77.20/24`. Both enabled adapters used the same private LAN segment. I checked guest addresses, routes, a non-packet route lookup and ICMP reachability.

## Method

1. Checked the VMware adapter settings and that no second adapter was enabled.
2. Assigned static addresses on `192.168.77.0/24` without a default gateway.
3. Read each guest's address and route state and looked up an outside-lab route without sending packets.
4. Pinged between the two owned guests.

## Results

Kali and the target each had only a connected IPv4 route. Kali had no IPv6 route. The target's IPv6 default entries were reject routes. Outside-lab route lookups failed. Pings succeeded three of three in both directions. This supports isolation for the recorded run; it does not prove every later VM state.

Evidence: [topology diagram](../../assets/images/lab-topology.svg), [Kali adapter screenshot](evidence/kali-lan-segment.png), [target adapter screenshot](evidence/target-lan-segment.png), [sanitised adapter settings](evidence/adapter-config-excerpt.txt), [Kali route screenshot](evidence/kali-routes-and-reachability.png), [Kali text excerpt](evidence/route-check.txt), [target text excerpt](evidence/target-route-check.txt).

[Screenshot provenance and hashes](../../EVIDENCE.md)

## Issue and next step

The target's older console did not accept automated text. A snapshot and configuration backup preceded temporary host-only management access for address setup. That extra path was removed before scanning. For the next lab, I would capture the adapter state before and after each temporary change in one dated checklist.

The network run was recorded on 16 November 2026. The VMware GUI screenshots were captured on 18 November 2026.

[View the project page](index.html)
