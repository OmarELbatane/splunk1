# ItsBitsy
Hello,



SOC Analyst Johny has observed some anomalous behaviours in the logs of a few windows machines. It looks like the adversary has access to some of these machines and successfully created some backdoor. His manager has asked him to pull those logs from suspected hosts and ingest them into Splunk for quick investigation. Our task as SOC Analyst is to examine the logs and identify the anomalies.


<h2> Question 1 </h2>

How many events were collected and Ingested in the index main?

<h2> Answer </h2>

We started first by researching and reporting.

To answer this question, all I have to do is set the query index to "main," change the time to "all time," and switch to verbose mode for the lecture.

<h2> Question 2 </h2>
On one of the infected hosts, the adversary was successful in creating a backdoor user. What is the new username?

<h2> Answer </h2>
I started by verifying the latest event IDs of everyone and found out that the event ID contains this information.

<h2> Question 3 </h2>
On the same host, a registry key was also updated regarding the new backdoor user. What is the full path of that registry key?
<h2> Answer </h2>
Since Sysinternals Sysmon is installed on the systems, we know from Sysmon that Event ID 12 is for registry object add/delete, Event ID 13 is for registry value set, and Event ID 14 is for registry key and value rename.

<h2> Question 4 </h2>
Examine the logs and identify the user that the adversary was trying to impersonate.

<h2> Answer </h2>
Here, all I had to do was go back and find the users, and so I found this information.

<h2> Question 5 </h2>

What is the command used to add a backdoor user from a remote computer?

<h2> Answer </h2>

Since Windows must run a process to add a new user, and each time a new process is created a log entry is added, there must be another log with a different Event ID containing the command that was executed. This Event ID is #1. By adding that value to our search, we are down to 25 logs: index="main" EventID="1"

<h2> Question 6 </h2>

How many times was the login attempt from the backdoor user observed during the investigation?

<h2> Answer </h2>

To answer this, all I need to do is use this command to find out how many times:
index="main" User="A1berto"

<h2> Question 7 </h2>

What is the name of the infected host on which suspicious PowerShell commands were executed?
<h2> Answer </h2>
This was easy to find since it's one of the hosts from the start.

<h2> Question 8 </h2>

PowerShell logging is enabled on this device. How many events were logged for the malicious PowerShell execution?

<h2> Answer </h2>

When I did my research, I found this:
"When PowerShell logging is enabled, Windows logs all PowerShell commands with event ID 4103."

So, I used this command and found that information.

<h2> Question 9 </h2>

An encoded PowerShell script from the infected host initiated a web request. What is the full URL?

<h2> Answer </h2>

To be honest, this was hard and took me some time to do, but I managed. Just note that I did some research and got some help before doing this.

So, I started first of all by copying all the text and putting it into CyberChef.

Inside the encoded code, we find this:

:Unicode.GetString([Convert]::FromBase64String('aAB0AHQAcAA6AC8ALwAxADAALgAxADAALgAxADAALgA1AA=='))), and we need to add /news.php at the end.

So now, I need to convert from base64 to string for aAB0AHQAcAA6AC8ALwAxADAALgAxADAALgAxADAALgA1AA==

And we get this URL: http://10.10.10.5/news.php

After defanging the URL and adding it, we get this result.

Thank you for your attention.
I learned in this challenge that I'm still far away from mastering Splunk, but it was still fun to try.



![Image Description](/sp2.png)





