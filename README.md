# rules.v6
ip6tables rules
```
-A INPUT -m state --state ESTABLISHED,RELATED -m comment --comment "statefull firewall" -j ACCEPT

-A INPUT -i lo -m comment --comment "allow from localhost" -j ACCEPT
-A INPUT -m udp -p udp --dport 546 -d fe80::/64      -m comment --comment "dhcpv6" -j ACCEPT
-A INPUT              -p ipv6-icmp --icmpv6-type 1   -m comment --comment "destination unreachable" -j ACCEPT
-A INPUT              -p ipv6-icmp --icmpv6-type 2   -m comment --comment "packet too big" -j ACCEPT
-A INPUT              -p ipv6-icmp --icmpv6-type 3   -m comment --comment "time exceeded" -j ACCEPT
-A INPUT              -p ipv6-icmp --icmpv6-type 4   -m comment --comment "parameter problem" -j ACCEPT
-A INPUT              -p ipv6-icmp --icmpv6-type 128 -m limit --limit 120/min -m comment --comment "echo request" -j ACCEPT
-A INPUT -s fe80::/10 -p ipv6-icmp --icmpv6-type 130 -m comment --comment "mcast listner query" -j ACCEPT
-A INPUT -s fe80::/10 -p ipv6-icmp --icmpv6-type 131 -m comment --comment "mcast listner report" -j ACCEPT
-A INPUT -s fe80::/10 -p ipv6-icmp --icmpv6-type 132 -m comment --comment "mcast listner done" -j ACCEPT
-A INPUT              -p ipv6-icmp --icmpv6-type 133 -m comment --comment "router solicitation" -j ACCEPT
-A INPUT              -p ipv6-icmp --icmpv6-type 134 -m comment --comment "router advertisement" -j ACCEPT
-A INPUT              -p ipv6-icmp --icmpv6-type 135 -m comment --comment "neighbor solicitation" -j ACCEPT
-A INPUT              -p ipv6-icmp --icmpv6-type 136 -m comment --comment "neighbor advertisement" -j ACCEPT
-A INPUT              -p ipv6-icmp --icmpv6-type 141 -m comment --comment "IND solicitation" -j ACCEPT
-A INPUT              -p ipv6-icmp --icmpv6-type 142 -m comment --comment "IND advertisement" -j ACCEPT
-A INPUT -s fe80::/10 -p ipv6-icmp --icmpv6-type 143 -m comment --comment "mcast listner report" -j ACCEPT
-A INPUT              -p ipv6-icmp --icmpv6-type 148 -m comment --comment "certification path solicitaion" -j ACCEPT
-A INPUT              -p ipv6-icmp --icmpv6-type 149 -m comment --comment "certification path advertisement" -j ACCEPT
-A INPUT -s fe80::/10 -p ipv6-icmp --icmpv6-type 151 -m comment --comment "multicast router advertisement" -j ACCEPT
-A INPUT -s fe80::/10 -p ipv6-icmp --icmpv6-type 152 -m comment --comment "multicast router solicitation" -j ACCEPT
-A INPUT -s fe80::/10 -p ipv6-icmp --icmpv6-type 153 -m comment --comment "multicast router termination" -j ACCEPT
-A INPUT              -p ipv6-icmp -m limit --limit 1/second --limit-burst 100 --log-prefix "dropped ICMPv6: " -j LOG
```
