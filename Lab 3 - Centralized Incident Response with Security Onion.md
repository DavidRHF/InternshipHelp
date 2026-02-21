# Detecting persistence through malicious service creation #
The following goes through attacks from Lab 1 and Lab 2. Instead of using Windows Event Viewer, we will be using Security Onion for a more natural scenario.

## *Step 1: The Attack (From Kali VM)* ##
Navigate to the Kali VM and run the commands seen in Lab 1 and Lab 2:

### Lab 1 attack: ###

- This time, we are going to be using the impacket tool to run 'whoami /all' in a shell

`impacket-smbexec lab.local/Administrator:'Passw0rd!'@<DC_IP>`

#### Inside shell, run: ####

`whoami /all`

### Lab 2 attack: ###

- Same as Lab 2 code

`impacket-psexec lab.local/Administrator:'Passw0rd!'@<DC_IP>`

#### Inside shell, run: ####

`sc create "Maintenance" binPath= "cmd.exe /c echo 'Backdoor' > C:\temp.exe"`

## *Step 2 Task A: The Investigation: Checking for High-Level Alerts* ##

Lets set up our filters to find our alerts: 
- Navigate to Security Onion
- Left sidebar &rarr; Alerts
- Options &rarr; Enable advanced interface features
- Filter to:
    - `event_data.host.name: "DC VM Name"`
    - Mine in this case is 






