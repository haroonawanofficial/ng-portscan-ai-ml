# Next-Generation Port Scanner

### Overview
The **Next-Generation Port Scanner** is an advanced, AI/ML-powered port scanning tool designed for comprehensive network analysis and evasion techniques. This tool integrates with custom tools like `nmap` and `hping`, or any custom TCP/IP written in python, perl, go, etc stealth techniques to bypass IDS/IPS defenses while providing detailed reports.

---

### Features
- **Advanced Scanning Techniques**: Supports ICMP, TCP, UDP, and custom payload-based scans.
- **Evasion Mechanisms**: Incorporates TTL manipulation, TCP window size adjustments, and fragmentation attacks.
- **Custom Tool Integration**: Seamlessly integrates with tools like `nmap` and `hping` for enhanced results.
- **AI/ML-Powered Adaptation**: Detects false positives and optimizes scan strategies using trained models.
- **Deep Packet Inspection (DPI)**: Analyzes network traffic to identify firewalls, IDS/IPS, and segment configurations.
- **Dynamic Reporting**: Generates detailed tabular and JSON reports, highlighting detected vulnerabilities and network configurations.

---

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

### Contributions
Contributions are welcome! Feel free to submit issues or pull requests.

### License
This project is licensed under the MIT License. See the LICENSE file for details.
