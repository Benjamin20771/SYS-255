## Lab 01 | Environment Setup

Step 1: Assign net0 to the WAN, which should not have your name assigned to it. Then, for net1, you should assign it to the LAN, which should have your name assigned to it.

WAN MAC Address:

<img width="466" height="59" alt="image" src="https://github.com/user-attachments/assets/621b0f64-9a73-496c-b49b-7b94f6071eaa" />

LAN MAC Address:

<img width="487" height="58" alt="image" src="https://github.com/user-attachments/assets/75a9236a-c72b-45c9-aa12-03d879109294" />

My WAN and LAN are either missing network configuration information or contain default IP addresses. Now is when we put them in

First, press 1 to configure the names of the WAN and LAN. Make sure MAC Addresses match up correctly. Say no to setting up VLANS first. Make sure vtnet0 is WAN and vtnet1 is LAN. 

#### WAN Setup:

Select 1 to pick the WAN interface

Do not use DHCP for the WAN IPv4 address

Enter your assigned WAN IP from the Network Assignments sheet in Canvas

You are using a 24-bit subnet mask

For the WAN, your upstream gateway is 10.0.17.2

Use the gateway as your IPv4 name server as well

We will not be using IPv6; please respond 'no' when asked about DHCP.

Press <ENTER> to bypass IPv6 configuration

Do not enable the DHCP server on the WAN

When asked about HTTP for the GUI, respond no (we want to use secure HTTPS)

#### LAN Setup:

Select 2 to pick the LAN interface

We are not using DHCP

Your LAN IP Address is 10.0.5.2.  This applies to every student.

You are using a 24-bit subnet mask

You do not have an upstream LAN gateway (you are the gateway for the LAN).  Press <ENTER>

No DHCPv6

Press <ENTER> to bypass IPv6 configuration

Do not enable a LAN DHCP Server

Do not revert to HTTP


