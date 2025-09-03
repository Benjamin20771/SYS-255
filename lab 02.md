## Lab 02 | DNS + ADDS Role

Firstly, we should assign the net0 to the LAN to make it assigned to our network and not anything else.

LAN MAC Address for ad01:

<img width="595" height="141" alt="image" src="https://github.com/user-attachments/assets/65726444-2929-4e52-8885-1fe257bc59ca" />

Navigate to the "Server Manager" and go to local Servers, and edit everything as follows
* IP Address:  10.0.5.5
* Netmask: 255.255.255.0
* Gateway 10.0.5.2 
* DNS 10.0.5.2
* Discoverable option.  If dialog shows up, select Yes for those systems on your LAN.
* Time should be set to UTC-5:00 Eastern Time (US & Canada)
* Computer name:  ad01-yourname (make sure you get this right). 
