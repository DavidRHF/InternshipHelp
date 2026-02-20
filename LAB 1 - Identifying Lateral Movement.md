# Identifying Lateral Movement #
The following goes through a simple attack that identifies privilages on another device.

## *Step 1: The Attack (From Kali VM)* ##
Navigate to the Kali VM and run this remote command on the DC:

`crackmapexec smb <DC_IP> -u Administrator -p 'Passw0rd!' -x 'whoami /all'`

---

#### What does this command do when broken down? ####

The security tool:
1. crackmapexec (CME)
   - Post-exploitation tool commonly used in penetration testing
- Legitimate uses:
   - Checking for weak credentials and password reuse
   - Red team testing for real attacker simulation
   - Blue team validation for tool verification and confirming that logging works
- Illegitimate uses:
  - Executing malicious payloads
  - Gaining Domain access

---

#### Entries after crackmapexec: ####

2. smb 
   - Determines the protocol to use
   - Is the Windows file-sharing and remote administration protocol.
   - Typically port 445
3. <DC_IP>
   - The target DCs IP address
   - In my case, my test DCs IP is 192.168.1.80
   - Important since the command needs a location to target
4. -u Administrator
   - Specifies the user being targeted
   - The command needs a specific user to authenticate as
   - Administrator is the intended user
5. -p 'Passw0rd!'
   - Specifies the password to the targeted account
   - Login will fail without proper credentials
   - Passw0rd! is the password for Administrator
6. -x 'whoami /all'
   - tells CME to execute the command remotely
   - whoami /all is the command being executed
   - The command outputs certain information about the security context of the logged-in account

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

---

*Used to record succesful authentication*

*It records a network logon which is normal for smb authentication*

#### Fields that connect to the event: ####

|Field|Log Value|Why does this matter?|
|---|---|---|
|Logon Type|3|Shows an SMB login|
|Account Name|Administrator|The account used for identification|
|Source Network Address|Kali IP (192.168.1.79)|Proves that another system ran the command|
|Authentication Package|NTLM|Is a remote authentication method|

*Event Viewer proof:*
![Picture 5](images/InternshipLab1-Photo5.png)
![Picture 6](images/InternshipLab1-Photo6.png)

---

### Event ID 4688 (Security Log) ###

---

*Records the creation of whoami.exe*

*Creation occurs under the authenticated session*

#### Fields that connect to the event: ####

|Field|Log Value|Why does this matter?|
|---|---|---|
|Creator Process Name|Typically services.exe or cmd.exe|Shows the process that created it|
|New Process Name|C:\Windows\System32\whoami.exe|File path showing location of process|
|Token Elevation Type|%%1936|Indicates full token access with no privilages removed|

### Before Event ID 4688 appears: ###

![Picture 7](images/InternshipLab1-Photo7.png)
![Picture 8](images/InternshipLab1-Photo8.png)

*Event Viewer proof:*

![Picture 9](images/InternshipLab1-Photo9.png)

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








