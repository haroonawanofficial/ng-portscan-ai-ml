# Next-Generation Port Scanner

### Overview
The **Next-Generation Port Scanner** is an advanced, AI/ML-powered port scanning tool designed for comprehensive network analysis and evasion techniques. This tool integrates with custom tools like `nmap` and `hping`, or any custom TCP/IP written in python, perl, go, etc stealth techniques to bypass IDS/IPS defenses while providing detailed reports.

### Features
- **Advanced Scanning Techniques**: Supports ICMP, TCP, UDP, and custom payload-based scans.
- **Evasion Mechanisms**: Incorporates TTL manipulation, TCP window size adjustments, and fragmentation attacks.
- **Custom Tool Integration**: Seamlessly integrates with tools like `nmap` and `hping` for enhanced results.
- **AI/ML-Powered Adaptation**: Detects false positives and optimizes scan strategies using trained models.
- **Deep Packet Inspection (DPI)**: Analyzes network traffic to identify firewalls, IDS/IPS, and segment configurations.
- **Dynamic Reporting**: Generates detailed tabular and JSON reports, highlighting detected vulnerabilities and network configurations.

### How Requests Look
- With simple Nmap (for example purpose but it can be any tool like hping or custom written in go, perl, python, c++, etc)
Here’s how a standard Nmap SYN scan request looks without script's integration:

 ```bash
IP(dst=192.168.1.1, ttl=64)/
TCP(dport=80, flags="S", options=[('MSS', 1460), ('WScale', 7), ('SAckOK', None)])

- TTL: Default TTL value (64).
- TCP Flags: SYN (`S`) flag to initiate a connection.
- Options: Standard TCP options like MSS, Window Scale, and SACK.
   ```

- With NG-PortScan ML and AI combined
Here’s how the combined request with script's `tcp_with_http` evasion and Nmap for port 80 would look:

```bash
IP(dst=192.168.1.1, ttl=128, options=[IPOption(b'\x01'*40)])/
TCP(dport=80, flags="S", window=8192, options=[('MSS', 1460), ('WScale', 7), ('SAckOK', None)])/
Raw(load="GET / HTTP/1.1\r\nHost: safe.com\r\n\r\n")


- TTL: Modified (e.g., 128).
- IP Options: Custom padding (`b'\x01'*40`) for evasion.
- TCP Flags: SYN (`S`) with custom `window=8192` and options.
- Payload: HTTP request injected by script.
```

### Responses
### **Responses Without Script (Only Nmap):**

#### **1. Open Port (SYN-ACK)**
```plaintext
IP(src=192.168.1.1, dst=192.168.1.100, ttl=64)/
TCP(sport=80, dport=12345, flags="SA", window=29200, options=[('MSS', 1460)])
```

#### **2. Closed Port (RST)**
```plaintext
IP(src=192.168.1.1, dst=192.168.1.100, ttl=64)/
TCP(sport=80, dport=12345, flags="R", window=0)
```

#### **3. Filtered Port (ICMP Response)**
```plaintext
IP(src=192.168.1.1, dst=192.168.1.100, ttl=64)/
ICMP(type=3, code=13)  # Destination unreachable, filtered.
```

### **Responses With Script (Integrated with Nmap and Evasion):**

#### **1. Open Port (SYN-ACK with Modified Options)**
```plaintext
IP(src=192.168.1.1, dst=192.168.1.100, ttl=64)/
TCP(sport=80, dport=12345, flags="SA", window=5840, options=[('MSS', 1460), ('Timestamp', (34567, 78901)), ('WScale', 10)])
```

#### **2. Closed Port (RST with Decoy TTL/Evasion)** 
```plaintext
IP(src=192.168.1.1, dst=192.168.1.100, ttl=254)/
TCP(sport=80, dport=12345, flags="R", window=0)
```

#### **3. Filtered Port (Custom ICMP Response)** 
```plaintext
IP(src=192.168.1.1, dst=192.168.1.100, ttl=64)/
ICMP(type=3, code=13, load="Filtered by advanced firewall.")  # Enhanced evasion detected.
```



### Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/yourusername/ng-portscanner.git
   ```

2. Navigate to the directory:
   ```bash
   cd ng-portscanner
   ```

3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

4. Usage
   ```bash
   python3 next-generation-portscan.py --target <IP_ADDRESS> --ports <PORTS> [options]
   python3 next-generation-portscan.py --target 192.168.1.1 --ports 80 --scans tcp_with_http
   python3 next-generation-portscan.py --target 192.168.1.1 --ports 80 --customtool "nmap -p {port} {target}"
   ```

5.Key CLI Options
   ```bash
--target: Specify target IP(s).
--ports: Comma-separated list of ports to scan.
--scans: Choose scan techniques (e.g., tcp_with_http, icmp_with_dns).
--evasion: Enable specific evasion techniques (e.g., random_ttl_icmp, ip_option_padding).
--customtool: Execute custom commands like nmap or hping.
--dpi: Enable deep packet inspection for detailed traffic analysis.
   ```

### Created by
Haroon Awan

### Comapny
cyberzeus.pk

### Email
Haroon@cyberzeus.pk

### Contributions
Contributions are welcome! Feel free to submit issues or pull requests.

### License
This project is licensed under the MIT License. See the LICENSE file for details.
