# Network Security Lab
Hands-on network security lab: built a virtual subnet, analysed live  DNS/TCP/UDP traffic with Wireshark, simulated TCP SYN flood and IP  spoofing attacks using hping3, then mitigated them with iptables  firewall rules. Covers the full attack-defence lifecycle end to end.

## Overview
A hands-on network security lab built using virtual machines, covering the full 
attack-defence lifecycle across 4 levels.

## Project Outline
- **Level 1:** Built a /23 subnet network between two VMs and verified connectivity 
  via ping and ifconfig
- **Level 2:** Captured and analysed live DNS, TCP, and UDP traffic using Wireshark 
  (including throughput and RTT graphs)
- **Level 3:** Simulated TCP SYN flood and IP spoofing attacks using hping3 — 
  caused measurable TCP stack exhaustion and system instability on the victim VM
- **Level 4:** Implemented iptables firewall rules (IP blocking, SYN rate limiting) 
  to fully mitigate the attacks

## Tools Used
`Wireshark` `hping3` `iptables` `tcpdump` `iperf3` `ifconfig`

## Key Takeaways
- Observed real TCP stack exhaustion during a live SYN flood attack
- Learned the difference between packet capture (Wireshark) and firewall-level 
  filtering (iptables)
- Demonstrated that rate-limiting SYN packets + IP blocking fully stabilised 
  the victim machine

## Reflection

One of the most striking moments in this lab was watching A.V's VM crash in 
real time during the SYN flood — it made the theory viscerally real in a way 
that no lecture could. It also highlighted an important nuance: a SYN flood with 
a spoofed IP is significantly harder to defend against than one from a known 
source, because the traffic superficially resembles legitimate connection attempts.

Working with Wireshark also shifted how I think about network traffic. Seeing 
DNS resolution complete in under 2ms, or watching TCP flow graphs show exactly 
when a connection degrades, gave me an intuitive feel for what "normal" looks 
like — which is essential context for spotting anomalies in a SOC environment.

The firewall section reinforced that defence is about layering: blocking a single 
IP is trivial to bypass via spoofing, but combining IP blocking with SYN rate 
limiting removed the attack surface almost entirely. It also made clear that 
Wireshark is a pre-firewall tool — a subtle but important distinction when 
verifying whether defences are actually working.
