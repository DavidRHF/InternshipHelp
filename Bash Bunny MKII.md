# Bash Bunny MKII #
*This device tricks computers by emulating a variety of USB devices such as keyboards, network adapters and storage drives. By deploying pre-written payloads in an insertable MicroSD chip, specific tasks can be forced onto another device. These payloads can trick computers into installing backdoors, network attacks and exfiltrating documents.*



how to use it

![Picture 1](images/BashBunnyMKII-Photo1.png)





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











