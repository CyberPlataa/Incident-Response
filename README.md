# Incident-Response
<a href="https://imgur.com/WFB2DYI"><img src="https://i.imgur.com/WFB2DYI.jpg" title="source: imgur.com" /></a>

## Introduction
I ran through the various incident alerts on my honeynet lab and referenced the IR playbook created by the lab creator Josh Madakor. 
<a href="https://imgur.com/DsNpCSn"><img src="https://i.imgur.com/DsNpCSnb.png" title="source: imgur.com" /></a>



## Brute Force Success Incident 186

<a href="https://imgur.com/ZjBMbrm"><img src="https://i.imgur.com/ZjBMbrm.png" title="source: imgur.com" /></a>

I clicked and investigated the Incident 186
<a href="https://imgur.com/koS6RdQ"><img src="https://i.imgur.com/koS6RdQ.png" title="source: imgur.com" /></a>


I ran the query: 
SecurityEvent
| where EventID == 4624

and found a long list of logs. I got 28 total successful brute force attempts in a short amount of time. All within seconds of each other. The IP address tied into the incident was the one activating my alerts for this sever alert though.

The next query I ran: 
SecurityEvent
| where EventID == 4624
| where IpAddress contains "89.248.163.27"

Allowed me to see purely the log information of these related incidents. 

<a href="https://imgur.com/TTd68pv"><img src="https://i.imgur.com/TTd68pvb.png" title="source: imgur.com" /></a>

I ran a quick google search. The incident didn't really give me clear cut answers and found this article on the internet: 
https://www.inversecos.com/2020/04/successful-4624-anonymous-logons-to.html

"If your server has RDP or SMB open publicly to the internet you may see a suite of these logs on your server's event viewer. Although these are showing up as Event ID 4624 (which generally correlates to successful logon events), these are NOT successful access to the system without a correlating Event ID 4624 showing up with an Account Name \\domain\username and a type 10 logon code for RDP or a type 3 for SMB. You can double check this by looking at 4625 events for a failure, within a similar time range to the logon event for confirmation.

The reason for this is because when a user initiates an RDP or SMB connection, the connection via RDP/SMB will be logged as a successful connection, BEFORE the user is prompted to enter their password. This means a successful 4624 will be logged for type 3 as an anonymous logon. When the user enters their credentials, this will either fail (if incorrect with 4625) or succeed showing up as another 4624 with the appropriate logon type and a username.
"
-Lina Lau

Throughout the incident and my googles I kept a log using azure. 
<a href="https://imgur.com/Y0gSgqd"><img src="https://i.imgur.com/Y0gSgqd.png" title="source: imgur.com" /></a>

The incident- to my judgement turned out to be a false positive. Due to the nature of the initation of and RDP connection. 
<a href="https://imgur.com/JcqnZ7b"><img src="https://i.imgur.com/JcqnZ7b.png" title="source: imgur.com" /></a>

I made a note that the nature of our VM and the NSG without a firewall to filter traffic is ultimately the cause of the incident/alert and I layed out the next steps to correct and hopefully fix the incident. 

The next incident I worked on was a privilege escalation. 
<a href="https://imgur.com/aZfOFuj"><img src="https://i.imgur.com/aZfOFuj.png" title="source: imgur.com" /></a>

I obviously am the reason for it... but until I get hired I AM PRETENDINGGGGG that this was a worker doing some sketchy looking activities. This user went on to do password resets, and messing with our keyvault. I closed out the incident as a benign positive. 

<a href="https://imgur.com/WSfIwP3"><img src="https://i.imgur.com/WSfIwP3.png" title="source: imgur.com" /></a>


The last incident I responded to (for this post) was the detection of malware. I closed it- I was testing EICAR files and spammed the attacks. I'll be posting that incident (where I'm creating this alert) at a later time. 

<a href="https://imgur.com/dtPoOxY"><img src="https://i.imgur.com/dtPoOxY.png" title="source: imgur.com" /></a>

##Conclusion
Documented, and closed out various different incidents involved in my honeynet lab. 
