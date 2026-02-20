# Detecting persistence through malicious service creation #
The following goes through an attack process of creating a system service that allows access after system reboots.

## *Step 1: The Attack (From Kali VM)* ##
Navigate to the Kali VM and run this remote command on the DC:

`impacket-psexec lab.local/Administrator:'Passw0rd!'@<DC_IP>`

When inside the remote shell, run:

`sc create "Maintenance" binPath= "cmd.exe /c echo 'Backdoor' > C:\temp.exe"`

---

#### What does this command do when broken down? ####
Lets start with the command that opens the shell.

The security tool:
1. impacket-psexec
   - Python based use of Microsofts PsExec functions
   - allows remote command execution and shell access
- Legitimate uses:
   - Attacker simulations and compromise scenarios
   - Executing diagnostic commandss when physical access is unavailable
- Illegitimate uses:
  - Remotely executing ransomware or malware
  - Using persistence to hide malicious code as legitimate services

---

#### Entries after impacket-psexec: ####

2. lab.local
   - Specifies the targeted Domain name
   - Required for creating a temporary service inside of the DC
3. /Administrator
   - Specifies the user being targeted
   - The command needs a specific user to authenticate as
   - Administrator is the intended user
4. :'Passw0rd!'
   - The colon shows where the username ends and where the password starts
   - Passw0rd! is the password for Administrator
   - Login will fail without proper credentials
5. <DC_IP>
   - The target DCs IP address
   - In my case, my test DCs IP is 192.168.1.80
   - Important since the command needs a location to target
Overall, this command does the following:
   - Authenticates over SMB using adequate credentials
   - creates a temporary service
   - starts the service
   - offers an interactive SYSTEM shell

*Once the command runs, the output should look similar to this:*
![Picture 1](images/InternshipLab1-Photo1.png)
![Picture 2](images/InternshipLab1-Photo2.png)
![Picture 3](images/InternshipLab1-Photo3.png)



## *Step 2: Evidence Investigation (On DC VM)* ##

### Where the logs are located in *Event Viewer* ###
- Windows Security Log: Windows Logs -> Security
- Sysmon Operational Log: Applications and Services Logs -> Microsoft -> Windows ->
Sysmon -> Operational

*An example Event Viewer page with an open Event log should look something like this:*
![Picture 4](images/InternshipLab1-Photo4.png)


### Event ID 4624 (Security Log) ###

*Used to record succesful authentication*

*It records a network logon which is normal for smb authentication*

---

#### ID 4624 fields that connect to the event: ####

##### Indicates network login #####
![Picture 5](images/InternshipLab1-Photo5.png)

##### Shows what account authenticated the command #####
![Picture 6](images/InternshipLab1-Photo6.png)

##### Shows the Kali IP as the source #####
![Picture 7](images/InternshipLab1-Photo7.png)

##### Shows protocol used #####
![Picture 8](images/InternshipLab1-Photo8.png)

---

### Event ID 4688 (Security Log) ###

*Records the creation of whoami.exe*

*Creation occurs under the authenticated session*

---

#### ID 4688 fields that connect to the event: ####

##### Indicates network login #####
![Picture 5](images/InternshipLab1-Photo5.png)

##### Shows what account authenticated the command #####
![Picture 6](images/InternshipLab1-Photo6.png)

##### Shows the Kali IP as the source #####
![Picture 7](images/InternshipLab1-Photo7.png)

##### Shows protocol used #####
![Picture 8](images/InternshipLab1-Photo8.png)

---

#### Event ID 1 (Sysmon Log) ####

*Records detailed process creation information*

*Somewhat of an extension of 4688*

---

#### ID 1 fields that connect to the event: ####

##### Indicates network login #####
![Picture 5](images/InternshipLab1-Photo5.png)

##### Shows what account authenticated the command #####
![Picture 6](images/InternshipLab1-Photo6.png)

##### Shows the Kali IP as the source #####
![Picture 7](images/InternshipLab1-Photo7.png)

##### Shows protocol used #####
![Picture 8](images/InternshipLab1-Photo8.png)

---
