🔥 Personal Firewall Using Python
📌 Overview

This project implements a lightweight personal firewall using Python. It monitors network traffic, filters packets based on predefined rules, blocks suspicious activity, and logs events for security auditing.

🎯 Objectives

Monitor incoming and outgoing network packets

Block traffic based on IP, port, and protocol rules

Log suspicious packets for analysis

Enforce firewall rules using iptables (Linux)

(Optional) Display live monitoring using a GUI

🛠️ Technologies Used

Python

Scapy

iptables (Linux)

Tkinter (optional GUI)

Python Logging module

⚙️ Installation
sudo apt update
sudo apt install python3-pip iptables
pip install scapy
📜 Firewall Rules
BLOCKED_IPS = ["192.168.1.100"]
BLOCKED_PORTS = [23, 445]
BLOCKED_PROTOCOLS = ["ICMP"]
🔍 Packet Sniffing Logic
from scapy.all import sniff, IP, TCP, UDP
import logging

logging.basicConfig(filename="firewall.log", level=logging.INFO)

def firewall(packet):
    if packet.haslayer(IP):
        src_ip = packet[IP].src

        if src_ip in BLOCKED_IPS:
            logging.info(f"Blocked IP: {src_ip}")
            return

        if packet.haslayer(TCP) and packet[TCP].dport in BLOCKED_PORTS:
            logging.info(f"Blocked TCP Port: {packet[TCP].dport}")
            return

        if packet.haslayer(UDP) and packet[UDP].dport in BLOCKED_PORTS:
            logging.info(f"Blocked UDP Port: {packet[UDP].dport}")
            return

sniff(prn=firewall, store=0)
🔐 iptables Enforcement (Linux)
sudo iptables -A INPUT -s 192.168.1.100 -j DROP
sudo iptables -A INPUT -p tcp --dport 23 -j DROP
sudo iptables -A INPUT -p icmp -j DROP
📊 Logging

Logs are stored in firewall.log

Includes blocked IPs, ports, protocols, and timestamps

🖥️ Optional GUI

Live packet monitoring

Blocked traffic display

Dynamic rule updates

✅ Final Outcome

A CLI/GUI-based personal firewall capable of detecting, blocking, and logging malicious network traffic at the host level.
