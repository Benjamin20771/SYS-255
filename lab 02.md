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

Now that that is done, we can close that out and then click on the yellow triangle and click promote. It's going to be new forest and the input is (ben.local). Enter a DSRM password that you will remember, and continue with defaults until installation. Ignore any error or leave as is.

