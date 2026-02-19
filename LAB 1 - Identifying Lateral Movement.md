# Identifying Lateral Movement #
The following goes through a simple attack that identifies privilages on another device.

### *Step 1: The Attack (From Kali VM)* ###
Navigate to the Kali VM and run this remote command on the DC:

`crackmapexec smb <DC_IP> -u Administrator -p 'Passw0rd!' -x 'whoami /all'`

#### What does this command mean when broken down? ####

1. crackmapexec
   -
2. smb
   -
3. DC_IP
   - This would be the target DCs IP address
   - In my case, my test DCs IP is 

Once the command runs, the output should look similar to this:
![Picture 1](images/InternshipLab1-Photo1.png)
![Picture 2](images/InternshipLab1-Photo2.png)
![Picture 3](images/InternshipLab1-Photo3.png)











### *Step 2: Evidence Investigation (On DC VM)* ###
Event ID 4624 (Security Log): Successful Network Logon (Type 3). Identify the Source Network
Address (Kali IP).
Event ID 4688 (Security Log): Process Creation for whoami.exe .
Event ID 1 (Sysmon Log): Detailed Process Creation. Locate the CommandLine field to see
