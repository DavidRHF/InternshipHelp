# Bash Bunny MKII #
*This device tricks computers by emulating a variety of USB devices such as keyboards, network adapters and storage drives. By deploying pre-written payloads in an insertable MicroSD chip, specific tasks can be forced onto another device. These payloads can trick computers into installing backdoors, network attacks and exfiltrating documents.*

If anybody gets confused, the link to the official Bash Bunny help page is right here:
[Bash Bunny Help](https://docs.hak5.org/bash-bunny/bash-bunny-by-hak5/)


## Steps to setting up the Bash Bunny MKII correctly ##

*Before looking into and executing attacks, we need to download the latest firmware onto the Bash Bunny. Thankfully, these steps are super simple.*

We need 2 specific pieces of hardware for this:
- Bash Bunny MKII
- MicroSD card

Insert the MicroSD card into your device for the download. 
Dowload the latest firmware from this page:
[Bash Bunny MKII Firmware](https://downloads.hak5.org/bunny/mk2)

- Once downloaded from the site, move it into the MicroSD card from your file browser.
- When done transferring into the file, extract the MicroSD card from your file system (For safety).
- Remove the MicroSD card from your device.

*The file should look something like this in your MicroSD*
![Picture 1](images/BashBunnyMKII-Photo1.png)

- Insert the MicroSD into the Bash Bunny MKII
- Insert the Bash Bunny MKII into the device
- Wait for the files to download onto the Bash Bunny
  - This could take some time. 2-5 minutes
  - The dowload is indicated 







![Picture 2](images/BashBunnyMKII-Photo2.png)



Must disable in removable storage access.
Make sure group policy editor is installed on your computer

- Win + r
- gpedit.msc
- Make sure it is installed

Removable Disks: 
- Deny execute access
- Deny write access

this is important since it will





how to interpret its output

explains everything needed to understand its use and output

how to detect it

## Possible Prevention Options ##
*There are multiple prevention techniques but it's important to remember that there is no perfect defense. Due to the way Bash Bunny MKII operates, many concrete defenses feature USB restrictions, policy, and endpoint protection.*

---
#### Disable or restrict unused ports ####
- Disable USB ports in BIOS/UEFI
- Use Group Policy or endpoint security tools to block unauthorized USB devices


#### Block or Monitor HID Devices ####
(Bash Bunny can act as a Human Interface Device (HID) to inject keystrokes like a keyboard)
- Block new keyboard devices from being added
- Use endpoint security tools for detecting strange keystroke activity


#### Network Adapter Monitoring ####
(Bash Bunny can emulate a USB Ethernet adapter and route traffic through itself)
- Monitor unusual DHCP or network interface changes
- Block automatic installation of new network adapters


#### Physical Security & User Training ####
- Teach users to avoid plugging in unknown USB drives
- Lock screens when leaving a workstation
---











