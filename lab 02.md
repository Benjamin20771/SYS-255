## Lab 02 | DNS + ADDS Role

Firstly, we should assign the net0 to the LAN to make it assigned to our network and not anything else.

LAN MAC Address for ad01:

<img width="595" height="141" alt="image" src="https://github.com/user-attachments/assets/65726444-2929-4e52-8885-1fe257bc59ca" />

Navigate to the "Server Manager" and go to local Servers, and edit everything as follows
* IP Address:  10.0.5.5
* Netmask: 255.255.255.0
* Gateway 10.0.5.2 
* DNS 10.0.5.2
* Discoverable option.  If the dialog shows up, select Yes for those systems on your LAN.
* Time should be set to UTC-5:00 Eastern Time (US & Canada)
* Computer name:  ad01-yourname (make sure you get this right). 

Server Manager should now look like this:

<img width="757" height="361" alt="image" src="https://github.com/user-attachments/assets/a2cf6628-a155-4e3a-8ff3-feba2ea65e9b" />

Now, click the "Manage" button, then select "Add Roles," and add Active Directory Domain Services. Please just keep everything default until you can click the ADDS. Choose the restart destination server option, and select yes on the confirmation dialog. Now let it install and look ahead to see what you need to do after this. Can you prep anything?

Now that that is done, we can close that out and then click on the yellow triangle and click promote. It's going to be a new forest, and the input is (ben.local). Enter a DSRM password that you will remember, and continue with defaults until installation. Ignore any error or leave as is.

You are then logging in as an Administrator (BEN/Administrator). You're DNS Server will now be 127.0.0.1. Host name should be ad01-ben, and you should be able to ping 10.0.5.2

Now we're going to make it so that it can ping the firewall. Go to DNS Manager and firstly, we go to the reverse lookup zone, but add a new zone for 10.0.5, and go to the forward lookup zone and add a new user (A or AAAA). Add fw01-ben IP 10.0.5.2. do the same for ad01-ben 10.0.5.5. Make sure to check and uncheck/recheck PTR.

We are going to create a named domain administrator account as well as a named non-privileged user account. Go to AD DS and go to ADUaC. Add a new user under ben.local. It will look something like 

* Ben 
* Deyot
* Ben Deyot (adm)
* ben.deyot-adm

Then, add the user to "Domain Admins." Make sure to have an adm one and a regular one.

### Jump to WKS01
Now we change the DNS to 10.0.5.5. Then we join the domain

* System
* Control Panel
* System and Security
* System
* System properties
* Change
* Domain = ben
* ben.deyot-adm
* Admin Password

Finalize by restarting your workstation

Move to Lab 03

