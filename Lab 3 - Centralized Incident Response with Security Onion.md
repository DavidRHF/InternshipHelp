# Detecting persistence through malicious service creation #
The following goes through attacks from Lab 1 and Lab 2. Instead of using Windows Event Viewer, we will be using Security Onion for a more natural scenario.

## *Step 1: The Attack (From Kali VM)* ##
Navigate to the Kali VM and run the commands seen in Lab 1 and Lab 2:

#### Lab 1 attack: ####

`impacket-smbexec lab.local/Administrator:'Passw0rd!'@<DC_IP>`
# Inside shell, run: whoami /all

#### Lab 2 attack: ####

`impacket-psexec lab.local/Administrator:'Passw0rd!'@<DC_IP>`

sc create "Maintenance" binPath= "cmd.exe /c echo 'Backdoor' > C:\temp.exe"
