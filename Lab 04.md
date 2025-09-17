

## Part 1: Setup PuTTY Connection

### 1. Disable IE Enhanced Security on AD01
1. Open **Server Manager**
2. Click **"Local Server"**
3. Click **"On"** next to **IE Enhanced Security Configuration**
4. Set both to **"Off"**
5. Click **OK**

### 2. Download and Install PuTTY
1. Open Internet Explorer on AD01
2. Go to `https://www.putty.org/`
3. Download and install PuTTY

### 3. Connect to DHCP01
1. Open PuTTY
2. **Host Name:** `dhcp01.yourname`
3. **Port:** 22
4. **Connection type:** SSH
5. Click **"Open"**
6. Log in with your credentials

---

## Part 2: Install and Configure DHCP

### 4. Install the DHCP Package
```bash
sudo dnf install dhcp-server -y
```

### 5. Backup and Edit Configuration
```bash
sudo -i
cp /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf.bak
vi /etc/dhcp/dhcpd.conf
```

### 6. Create DHCP Configuration
**Clear file and add this configuration:**
```
default-lease-time 600;
max-lease-time 7200;
authoritative;

subnet 10.0.5.0 netmask 255.255.255.0 {
    range 10.0.5.101 10.0.5.125;
    option domain-name "yourname.local";
    option domain-name-servers 10.0.5.2;
    option routers 10.0.5.1;
    option broadcast-address 10.0.5.255;
}
```

**Save and exit vi:** Press `Esc`, type `:wq`, press `Enter`

### 7. Test Configuration
```bash
dhcpd -t
```

### 8. Start and Enable DHCP Service
```bash
systemctl start dhcpd
systemctl enable dhcpd
systemctl status dhcpd
```

### 9. Configure Firewall
```bash
firewall-cmd --permanent --add-service=dhcp
firewall-cmd --reload
firewall-cmd --list-all
```

### 10. Exit Root Mode
```bash
exit
exit
```

---

## Part 3: Configure Windows Client

### 11. Change WKS01 to DHCP
1. Open **Network and Sharing Center**
2. Click **"Change adapter settings"**
3. Right-click **Ethernet adapter** → **Properties**
4. Select **"Internet Protocol Version 4 (TCP/IPv4)"** → **Properties**
5. Select **"Obtain an IP address automatically"**
6. Select **"Obtain DNS server address automatically"**
7. Click **OK** twice

### 12. Verify DHCP Assignment
```cmd
ipconfig /all
```

---

## Part 4: Check DHCP Logs

### 13. View DHCP Logs on dhcp01
```bash
sudo cat /var/log/messages | grep wks01-ben
```

---

## Part 5: Wireshark DHCP Capture

### 14. Start Wireshark on WKS01
1. Open **Wireshark**
2. Start capture on **Ethernet0**

### 15. Release and Renew DHCP
```cmd
ipconfig /release
ipconfig /renew
```

### 16. Analyze Wireshark Traffic
1. Stop capture
2. Apply filter: `udp.port == 67 or udp.port == 68`
3. Examine the 4 DHCP messages: DISCOVER, OFFER, REQUEST, ACK

---

## Part 6: Modify Lease Times

### 17. Change Lease Times
```bash
sudo vi /etc/dhcp/dhcpd.conf
```

**Change these lines:**
```
default-lease-time 3600;    # 1 hour
max-lease-time 14400;       # 4 hours
```

### 18. Restart DHCP Service
```bash
sudo systemctl restart dhcpd
sudo systemctl status dhcpd
```

---


## Quick Reference Commands

### DHCP Service Management
```bash
sudo systemctl start/stop/restart dhcpd
sudo systemctl status dhcpd
sudo dhcpd -t
```

### Log Analysis
```bash
sudo cat /var/log/messages | grep dhcp
sudo tail -f /var/log/messages
```

### Windows DHCP Commands
```cmd
ipconfig /all
ipconfig /release
ipconfig /renew
```

### Firewall Management
```bash
sudo firewall-cmd --list-all
sudo firewall-cmd --permanent --add-service=dhcp
sudo firewall-cmd --reload
```

---

## Troubleshooting Tips

**If DHCP service fails:**
1. Check syntax: `sudo dhcpd -t`
2. Check logs: `sudo journalctl -u dhcpd`
3. Verify firewall: `sudo firewall-cmd --list-all`

**If client doesn't get IP:**
1. Verify DHCP service running: `sudo systemctl status dhcpd`
2. Check client is on correct network
3. Verify firewall allows DHCP traffic

**Restore from backup if needed:**
```bash
sudo cp /etc/dhcp/dhcpd.conf.bak /etc/dhcp/dhcpd.conf
sudo systemctl restart dhcpd
```
