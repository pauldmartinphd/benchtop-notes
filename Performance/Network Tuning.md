## TCP Congestion Control

### /etc/sysctl.d/40-network.conf
    #Select TCP CUBIC congestion control algorithm for LAN
	net.ipv4.tcp_congestion_control = cubic
	net.core.default_qdisc = fq_codel

	# Ubisoft fix from Universal Blue
     net.ipv4.tcp_mtu_probing = 1
[Link](https://www.reddit.com/r/linux_gaming/comments/10oc0dq/psa_for_people_having_trouble_connecting_to/)
[Link](https://blog.cloudflare.com/http-2-prioritization-with-nginx/)

### CUBIC vs. BBR Considerations
CUBIC (the current setting) is the Linux default and works well for most LAN and general internet use. BBR (and the newer BBRv3) is Google's congestion control algorithm designed to maximize throughput on lossy, high-bandwidth networks. CachyOS ships BBRv3.

Trade-offs:
* **CUBIC** — Fair to other flows, well-tested, safe default. Best for LAN and low-latency scenarios.
* **BBRv3** — Better throughput on lossy/high-latency links (long-haul internet, WiFi), but can be unfair to CUBIC flows sharing the same bottleneck. Requires `fq` (fair queueing) as the qdisc, not `fq_codel`.
* For a desktop distro, CUBIC + fq_codel is the safer default. Consider BBRv3 as an optional profile or for users who report poor throughput on WiFi/WAN.

To switch to BBR (if desired):
    net.ipv4.tcp_congestion_control = bbr
    net.core.default_qdisc = fq

## DNS

### /etc/NetworkManager/conf.d/dns.conf
	[main]
	dns=systemd-resolved