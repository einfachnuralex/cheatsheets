# tcpdump

### Capture the traffic of a specific interface:

`tcpdump -i {{eth0}}`

### Capture all TCP traffic showing contents (ASCII) in console:

`tcpdump -A tcp`

### Capture the traffic from or to a host:

`tcpdump host {{www.example.com}}`

### Capture the traffic from a specific interface, source, destination and destination port:

`tcpdump -i {{eth0}} src {{192.168.1.1}} and dst {{192.168.1.2}} and dst port 80`

## Capture the traffic of a network:

`tcpdump net {{192.168.1.0/24}}`

### Capture all traffic except traffic over port 22 and save to a dump file:

`tcpdump -w dumpfile.pcap not port 22`

### Read dumpfile

`tcpdump -qns 0 -X -r dumpfile.pcap`

# Simple call

```
tcpdump -n -vv -e -i eth1
```

* -n: no lookup names
* -vv: more verbose
* -i: only this interface
* -e: print ethernet header

# Filter for dst host

```
tcpdump -n -i eth1 -e not dst host 224.0.0.18
```

* not dst host: do not show this host

## Filter not vrrp

```
tcpdump -n -i eth1 -e not vrrp
```

# Filter for vlan

https://serverfault.com/questions/196250/tcpdump-capture-one-of-several-vlans

```
tcpdump -vv -i eth1 '( vlan and ( ether[14:2] & 0xfff == 1000 or ether[14:2] & 0xfff == 501 ) ) and ( ip host 10.1.1.98 or ip host 10.1.1.99 )'
```

```
tcpdump -n -i eth1 -e | grep "vlan 1000"
```

# tcpdump expressions

```

TCPDUMP expressions

TCPDUMP expressions are also known as BPF, or Berkeley Packet Filters. On a TCPDUMP command line it is recommended to place them inside single quotes (UNIX) or double quotes (Windows) to avoid confusion and possible parsing errors.
Expressions

tcpdump "host profl"
    dumps all packets to or from host profl
tcpdump "ether host 11:22:33:44:55:66"
    dumps all packets to or from that MAC address
tcpdump "net 192.168.12.4/30"
    dumps all packets to or from a network, specified using CIDR notation
tcpdump "net 192.168.12.4 mask 255.255.255.252"
    dumps all packets to or from a network, specified using a mask
tcpdump "tcp src port 53"
    dumps all packets with source port 22/tcp
tcpdump "host {thisIP}"
    Show only IP traffic to or from thisIP
tcpdump "host {thisIP} && host {thatIP}"
    Show only IP traffic between thisIP and thatIP
tcpdump "!(host {myIP}) && {remainder of expression}"
    Ignore traffic from myIP (necessary if you're running TCPDUMP on a remote machine to stop it from capturing the terminal session with your machine)

Primitives

icmp[0]
    Show only echo reply
tcp[13] & 3 != 0
tcp[tcpflags] & (tcp-syn | tcp-fin) != 0
    show only SYN or FIN packets
tcp[13] & 0x12 != 0
tcp[tcpflags] & (tcp-syn & tcp-ack) != 0
    show only SYN/ACK packets
tcp[tcpflags] & (tcp-syn | tcp-fin | tcp-rst) != 0
    show SYN, FIN, and RST packets
ip[2,2] > 576
    show only packets longer than 576 bytes
icmp[0] = 3 and icmp[1] = 4
    Show ICMP type 3, code 4 (Needs fragmenting but DF bit set)
ip[6] & 0x40 = 0x40
    Show only IP packets with DF bit set
vlan && ip
    Show only IEEE 802.1q IP packets. Changes the decoding offsets for the remainder of the expression, as if the VLAN header had been stripped away.
vlan 186 && ip
    Show only IP packets in IEEE 802.1q VLAN number 186.

Assorted

ip proto 50
    Show only ESP packets (IP protocol 50)
ip proto 112
    show only VRRP packets (IP protocol 112)
proto vrrp
    all VRRP packets (works on IPSO)
```
