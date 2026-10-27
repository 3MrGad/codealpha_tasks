# CodeAlpha Tasks — Network Packet Sniffer

Work completed during a CodeAlpha cybersecurity internship.

## `packetsniffer.py`

A raw-socket packet sniffer that captures Ethernet frames straight from the NIC
and parses them layer by layer, printing a readable breakdown of each packet:

- **Ethernet:** destination MAC, source MAC, protocol
- **IPv4:** version, header length, TTL, protocol, source and target IP
- **ICMP:** type, code, checksum
- **TCP:** source/destination ports, sequence and acknowledgement numbers, flags (URG/ACK/PSH/RST/SYN/FIN)
- **UDP:** source/destination ports, length
- Payload data, formatted in aligned multi-line hex-ish output

It uses only the Python standard library (`socket`, `struct`, `textwrap`).

## Running

Raw sockets need root, and `AF_PACKET` is Linux-only:

```bash
sudo python3 packetsniffer.py
```

Press `Ctrl+C` to stop. On a busy interface the output is verbose — pipe it to a
file or `grep` for what you care about.

## What I learned

Parsing protocols by hand (unpacking headers with `struct`, masking out fields
like the IP header length and the TCP flag bits) made the packet structures
concrete in a way that reading an RFC diagram doesn't — which is directly useful
when reading traffic in Wireshark or Burp during a test.
