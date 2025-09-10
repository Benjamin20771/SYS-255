## Step 1: Configure dhcp01 Network Settings

In Proxmox: Configure dhcp01's network adapter to use your LAN segment (same as wks01)

Power on dhcp01 and log in as champuser (use the default password from Canvas)

## Step 2: Get Admin Privileges for champuser

Check current groups: groups champuser

Try to get sudo access (try these methods in order):
Try if champuser already has some sudo:
sudo usermod -aG wheel champuser

Log out and back in for group changes to take effect:
* exit
* Log back in as champuser
Test sudo access:
* sudo whoami
* Should return "root"

## Step 3: Configure Networking

* nmtui
* Select "Edit a connection"
* Configure these settings:

* IP: 10.0.5.3/24
* Gateway: 10.0.5.2
* DNS: 10.0.5.5
* Search domain: [ben].local

Set hostname on nmtui:
dhcp01-[ben]


## Step 4: Create Your Named User
* Add your named user 
sudo adduser [ben]

* Set password for the user
sudo passwd [ben]

* Add user to wheel group (gives sudo privileges)
sudo usermod -aG wheel [ben]

## Step 5: Test Networking 

Switch to your named user:
* su - [yourname]

Test connectivity:
* ping google.com
* ping ad01
* ping fw01

## Step 6: Add DNS Records 

On ad01 (Windows Server), open DNS Manager and Add A record:

* Right-click your domain zone ([ben].local)
* New Host (A or AAAA)
* Name: dhcp01
* IP: 10.0.5.3
* Check "Create associated pointer (PTR) record"


Test from wks01:
cmd-ping dhcp01

## Step 7: SSH Access (Deliverable 3)

From wks01, open Command Prompt or PowerShell
* Connect via SSH:
* cmdssh [yourname]@dhcp01
* Type "yes" to accept the certificate
* Enter your password

