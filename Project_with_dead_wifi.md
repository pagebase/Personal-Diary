# :rocket: Projects with dead Wi-Fi router
## Section A:
- **Practice Hardware Hacking via UART:** Open the case and look for a cluster of 3 or 4 pins (Tx, Rx, GND). You can connect a USB-to-TTL serial adapter to these pins to access the router's bootloader and root console. It is fantastic practice for exploring device security and reverse engineering.
 - **Flash Custom Firmware (OpenWrt/DD-WRT):** If you can get it on the network, flash it with open-source firmware. You can use it as a lightweight sandbox to run Python automation scripts, cron jobs, or manage local network processes without tying up your main PC.
 - **Set Up a Honeypot:** Isolate the router on a secure VLAN and set it up as a dummy target on your network. You can practice monitoring network traffic, analyzing packet captures, or safely testing out network vulnerability scanners against it.
 - **DIY Print or File Server:** If the router has a working USB port, you can plug in an old printer or a flash drive and configure it to serve files or print jobs to your local network.
If the Board is Completely Dead (Salvaging Parts)
If the main SoC (System on a Chip) is fried, it is time to harvest the hardware.
 - **Extract the Firmware (EEPROM):** Locate the flash memory chip (usually an 8-pin SOIC chip). You can practice desoldering it from the board, hook it up to an EEPROM programmer (like a CH341A), and attempt to dump the binary file to analyze its file system and look for hardcoded credentials.
 - **Repurpose the Antennas:** Wi-Fi antennas use standard IPEX/U.FL connectors. You can easily snap them off the board and reuse them to boost the range of custom IoT projects, ESP32 boards, or Software Defined Radio (SDR) setups for capturing wireless signals.
 - **Scavenge the Heatsinks:** The CPU and Wi-Fi chips usually have small ceramic or aluminum heatsinks. Carefully pry them off and clean the thermal paste. They are perfect for cooling down a Raspberry Pi or other small microcontrollers if you are pushing their hardware performance.
 - **Keep the Power Supply:** The wall adapter is usually a reliable 9V or 12V DC power supply. Keep it in your parts bin; it is incredibly useful for powering custom desktop gadgets, LED strips, or motor controllers.
 - **Desoldering Practice:** If you want to get better at soldering, a dead motherboard is a risk-free practice zone. Practice safely removing capacitors, LEDs, voltage regulators, and tactile buttons without lifting the copper pads.

## Section B:
Repurposing an old Wi-Fi router is a fantastic way to learn about embedded systems, networking, or basic electronics. Depending on your comfort level with software and soldering, you can either flash new life into the existing hardware or completely tear it apart for parts.
Here is a breakdown of the best projects you can do with a router's hardware, ranging from software hacks to complete teardowns.
1. Firmware & Repurposing (No Soldering Required)
If the hardware is still functional, the best project is usually replacing the manufacturer's restricted software with an open-source Linux distribution.
 - **Install OpenWrt or DD-WRT:** This gives you root access to the router's Linux operating system. You can unlock advanced routing features that usually only come on enterprise-grade hardware.
 - **Create a Wi-Fi Repeater/Bridge:** Extend your current Wi-Fi network to a dead zone in your house by turning the old router into a wireless bridge.
 - **Build a Cheap NAS (Network Attached Storage):** If your router has a USB port, install OpenWrt, plug in an external hard drive, and configure it as a network drive for cheap local file storage and backups.
 - **Network-Wide Ad Blocker or VPN Server:** Run software on the router to block ads for every device connected to it, or set it up as a VPN server so you can securely access your home network remotely.
2. Hardware Hacking & Modding
If you want to actually modify the physical hardware, old routers are great for learning embedded security and electronics.
 - **UART/Serial Hacking:** Most router printed circuit boards (PCBs) have unpopulated pads for a serial console (UART). By finding these pins and soldering headers to them, you can connect a USB-to-TTL adapter and watch the router boot up, interrupt the bootloader, and get a root shell. This is exactly how cybersecurity researchers look for vulnerabilities in IoT devices.
 - **Cooling Mods:** Many older routers overheat under heavy load. You can cut the casing, add internal heat sinks to the main System-on-Chip (SoC), and wire up a small 5V or 12V PC fan directly to the router's internal power delivery.
 - **Antenna Upgrades:** If your router has internal antennas or non-removable ones, you can drill holes in the case, solder U.FL to SMA pigtail cables to the board, and attach massive high-gain external antennas.
3. Scavenging for Parts (Teardown Projects)
If the router is completely bricked or too old to be useful (like an old 802.11g model), it is a great donor board for other electronics projects.
 - **Build a "Cantenna":** Harvest the antennas and connectors to build a highly directional Wi-Fi antenna out of a metal soup can. This can shoot a Wi-Fi signal over surprisingly long distances.
 - **Desoldering Practice:** Router PCBs are packed with useful components for Arduino or Raspberry Pi projects. You can harvest:
   - Ethernet jacks (magjacks with built-in transformers).
   - Capacitors, resistors, and diodes.
   - LEDs and tactile push buttons (from the reset or WPS buttons).
   - Voltage regulators (useful for stepping down power in other projects).
 - **Repurpose the Enclosure:** Gut the PCB entirely and use the sleek plastic casing to house a Raspberry Pi cluster, a custom IoT sensor hub, or an Arduino project. The pre-cut holes for ethernet ports and power cables are very convenient.
**Safety Note:** Always ensure the router is unplugged before opening it up. While routers use low-voltage DC power internally, the capacitors can still hold a mild charge, and you should never open the actual "wall wart" power supply that plugs into the AC outlet.
