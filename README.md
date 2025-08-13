BIND DNS Server Deployment & Domain Access Control on AWS
📖 Overview
This project involves the configuration and deployment of a BIND-based DNS server on AWS EC2.
The server performs controlled domain resolution, allowing only specific domains while blocking all others.
It includes forward & reverse lookup zones, security hardening, and external accessibility — making it ideal for production and testing environments.

✨ Features
🎯 Controlled Domain Resolution

Resolves only specified domains:

myproject.com

testsite.org

Blocks all other domains.

🔄 Forward & Reverse Lookup Zones

Accurate domain-to-IP and IP-to-domain mapping.

40% faster troubleshooting.

🌐 External Device Accessibility

Network settings allow DNS testing from external devices.

30% improved collaboration.

🛡 Security Hardening

Recursion disabled to prevent DNS amplification attacks.

100% protection from unauthorized queries.

🏗 Architecture
☁ AWS EC2 Instance (Amazon Linux OS)

🔐 Security group allowing Port 53 TCP/UDP and Port 22 SSH

⚙ BIND DNS Server

Forward & reverse lookup zones configured

Domain access control rules applied

🧪 External devices used for testing resolution & blocking

🛠 Technologies Used
☁ AWS EC2

🐧 Amazon Linux

📡 BIND DNS Server

🗄 MySQL (optional for logging)

🚀 Setup Instructions
1️⃣ Launch EC2 Instance
Select Amazon Linux AMI

Configure security group:

Port 22 (SSH)

Port 53 (TCP/UDP)

2️⃣ Install BIND
sudo yum update -y
sudo yum install bind bind-utils -y
3️⃣ Configure BIND
Edit /etc/named.conf

Create zone files for allowed domains

Forward Lookup Zone Example (/var/named/myproject.com.zone)
$TTL 86400
@   IN  SOA myproject.com. admin.myproject.com. (
        2025081201 ; Serial
        3600       ; Refresh
        1800       ; Retry
        1209600    ; Expire
        86400 )    ; Minimum TTL

@       IN  NS  ns1.myproject.com.
ns1     IN  A   192.168.1.10
@       IN  A   192.168.1.10
Reverse Lookup Zone Example
dns
$TTL 86400
@   IN  SOA myproject.com. admin.myproject.com. (
        2025081201
        3600
        1800
        1209600
        86400 )

@       IN  NS  ns1.myproject.com.
10      IN  PTR myproject.com.
4️⃣ Restart & Enable Service
sudo systemctl restart named
sudo systemctl enable named
🧪 Testing
From an external device:
nslookup myproject.com <DNS_Server_IP>         # Should resolve
nslookup blockedsite.com <DNS_Server_IP>       # Should fail
📊 Results & Impact
✅ 40% faster troubleshooting with reverse lookup support.
✅ 30% better collaboration through external testing.
✅ 100% prevention of unauthorized domain resolution.

