# fix_all_errors_cant_join_to_domaine-windows-server-2022

<h3> But first you have to check if the dns name is correct,the 2 machine are in the same network by : <code>ping 'your-target-ip-address' </code> </h3>
- check the time&date in the 2 machine are correct like your home os date&time.<br>
- check your computer-name is changed (client-windows)<br>
- check your windows version is not home version may be entreprise version.<br>
- in your VM check in the network area you have apply <code> attached to Bridge-Nat </code> : depend on the vm you are using.<br>
  
if everything is correct but there is no-connection between the server and the clients you have to do that : <br>

<code> Go to Control Panel > System and Security > Windows Defender Firewall > Advanced Settings.<br>
On both machines, enable "File and Printer Sharing (Echo Request - ICMPv4-In)" for all profiles (Domain, Private, and Public).<br>
Ensure that the rule is enabled. </code><br>

Steps to Join WS10 to the Domain <br>
1. Verify DNS Configuration <br>
Ensure that the DNS server IP address on the WS10 machine is set to the IP of the WS-Server (which is running ADDS and DNS). 
How to Check: <br>
Go to Control Panel > Network and Sharing Center > Change adapter settings. <br>
Right-click on your network adapter and select Properties. <br>
Select Internet Protocol Version 4 (TCP/IPv4) and click Properties. <br>
Ensure the Preferred DNS server is set to the IP address of your WS-Server. 
Leave the Alternate DNS server blank. <br>
2. Check ADDS and DNS Health on WS-Server
Make sure the ADDS and DNS roles are correctly installed and running on WS-Server. 
Commands to Check ADDS Health on WS-Server:<br>

<ocde> nslookup </code>  ==> must return you the name of the dns server exists in you ws-server 
 if not :  <br>
 3. Ensure Network Discovery is Enabled
On both WS10 and WS-Server:
Go to Control Panel > Network and Sharing Center > Advanced sharing settings.
Turn on Network Discovery and File and Printer Sharing for the active network profile.
4. Verify Domain Connectivity from WS10
On WS10 client, open a command prompt and run: <br>
<code>
ping <domain_name>
nslookup <domain_name>
</code> <br>

5. Join the Domain <br>
Go to Settings > Accounts > Access work or school.
Click Connect and choose Join this device to a local Active Directory domain.
Enter the domain name (e.g., mydomain.local).
Provide the credentials of a domain user with permission to join devices to the domain.
Restart WS10 when prompted. <br>

if it still the same error : 
disable firewall in the 2 machine server and client with this command :  <br>
<code>
netsh advfirewall set allprofiles state off
</code> <br>

# in this case if you run <code> nslookup 'your-domaine' </code>  ,and it result you the dns name of your local home internet provider 

use this commands in the client machine: <br>
<code>
ipconfig /flushdns
ipconfig /registerdns
</code> <br>

and also if it the same you can diasble the service of ipv6 in the client machine  <br>

after return the task 5 and it will run with success. 
