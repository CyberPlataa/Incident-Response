# Incident-Response

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

