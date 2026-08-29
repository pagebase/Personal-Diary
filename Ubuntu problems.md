1. **Brightness slider missing in 24.04 version:**

#### Solution:
- Install latest GPU drivers by following command:
```bash
sudo ubuntu-drivers install
```
- Reboot system and your problem would be fixed.

---
2. **How to check available drivers?:** 

#### Solution

- Type following command:
```bash
ubuntu-drivers devices
```

---
3. **Bluetooth not turning on:**

#### Solution:

Bluetooth issues on Ubuntu are usually caused by a stopped service, a software block, or a glitch in the Bluetooth daemon (`bluez`).

  

Here is the standard process to force Bluetooth to turn back on using the terminal.

  

**1.Check for software blocks:**Unblock the radio transmitter.

Ubuntu has a tool called `rfkill` that manages wireless transmitters. Sometimes Bluetooth gets "soft blocked" by the system.

Open your terminal (`Ctrl` + `Alt` + `T`) and run:

  

Bash

```
sudo rfkill unblock bluetooth
```

Then, check the status:

  

Bash

```
sudo rfkill list
```

Ensure that both "Soft blocked" and "Hard blocked" say **no** for your Bluetooth device. _(If it says "Hard blocked: yes", you might have a physical switch or a keyboard shortcut, like Fn+F3, turned off)._

  

**2.Restart the Bluetooth service:**

Often, the background service managing Bluetooth just needs a reboot. Run this command:

  

Bash

```
sudo systemctl restart bluetooth
```

After running it, try toggling Bluetooth on from your top right system menu.

  

**3.Verify the service is running:**Check for crash errors.

If it still won't turn on, check what the service is currently doing:

  

Bash

```
sudo systemctl status bluetooth
```

You should see an "Active: **active (running)**" line in green. If it says "failed" or "inactive", press `q` to exit the status screen, and proceed to the next step.

  

**4.Reinstall the Bluetooth stack:**Fix missing or corrupted packages.

If the service is failing, the underlying packages might be corrupted or missing. Reinstall the core Bluetooth management tool (`bluez`):

  

Bash

```
sudo apt update
sudo apt install --reinstall bluez
```

Once the installation finishes, reboot your computer. You can start bluetooth service at startup for every time when you boot system by following command:

```bash
sudo systemctl enable bluetooth
```
If you want to enable it for future startups **and** start the service right now without rebooting, add the `--now` flag:

```bash
sudo systemctl enable --now bluetooth
```

---
# 4. How to control screen brightness through terminal command in Ubuntu and set 50% at startup?

The most reliable tool for controlling screen brightness via the terminal in Ubuntu is `brightnessctl`, as it works natively with both Wayland and X11 display servers.
Here is how to install it, test it, and create a custom service to force your screen to 50% on every boot.

**1.Install brightnessctl:**

Open your terminal and install the utility from the official repositories:

Bash

```
sudo apt update && sudo apt install brightnessctl
```

**2.Test the command:**

Verify the tool works on your display right now:  

Bash

```
brightnessctl set 50%
```

**3.Create a startup service:**

Ubuntu natively restores your _last used_ brightness on reboot. To override this and force exactly 50% every time, create a new systemd service:  

Bash

```
sudo nano /etc/systemd/system/set-brightness.service
```

Paste the following configuration into the file:

```
[Unit]
Description=Set screen brightness to 50% at startup
After=multi-user.target

[Service]
Type=oneshot
ExecStart=/usr/bin/brightnessctl set 50%

[Install]
WantedBy=multi-user.target
```

Save and exit the editor (in Nano: press `Ctrl+O`, `Enter`, then `Ctrl+X`).  

**4.Enable the service:**

Activate your new service so it runs automatically during the next boot:  

Bash

```
sudo systemctl enable set-brightness.service
```

> **Note on alternative GUI method:** If you prefer not to use `systemd`, you can also achieve this by opening Ubuntu's built-in **"Startup Applications"** program, clicking **Add**, and pasting `brightnessctl set 50%` into the Command field. Both methods work perfectly.

---
# 5. What is `Display servers`?

A display server is the foundational software in a Linux operating system that draws the graphical user interface (GUI) on your monitor and routes your mouse and keyboard inputs to the correct applications.  

Without a display server, your computer would just be a black screen with white text (a pure command-line interface).  

Think of it as a **traffic cop for your screen**. When you have a web browser and a terminal open side-by-side, the display server takes the visual data from both applications, calculates exactly where those windows belong on your monitor, and tells your graphics card how to render the final image. It also ensures that when you click a button, that click is routed exactly to the app your mouse is hovering over.
### The Two Main Linux Display Servers

Because Linux is open-source, there are two competing display server protocols in use today:

|**Feature**|**X11 (X.Org)**|**Wayland**|
|---|---|---|
|**Status**|The old standard. Created in the 1980s and patched heavily over the decades.|The modern replacement. Built specifically for today's graphics hardware.|
|**Security**|Weak. By design, any running application can see what other applications are doing, making keyloggers and unauthorized screen recording a risk.|Strong. Applications are strictly isolated from each other. An app must explicitly ask the system for permission to record the screen.|
|**Performance**|Prone to visual screen tearing and struggles with mixed-refresh-rate multi-monitor setups.|Smoother animations, less screen tearing, and native support for scaling across multiple displays.|
|**Current Usage**|Phasing out, but still used as a fallback for older software or specific NVIDIA hardware setups.|The default display server on modern Ubuntu, Fedora, and most major Linux distributions.|
#### How do I check if my Ubuntu system is currently using Wayland or X11?

```bash
echo $XDG_SESSION_TYPE
```

---
# 6. How to install different `Desktop Environment` and delete?

#### 1. KDE Plasma (Kubuntu)

A highly customizable, modern, Windows-like environment.

- **Install:** `sudo apt install kubuntu-desktop`
    
- **Delete:** `sudo apt remove kubuntu-desktop plasma-workspace sddm && sudo apt autoremove`
    

#### 2. XFCE (Xubuntu)

Extremely lightweight and fast, perfect for older hardware.

- **Install:** `sudo apt install xubuntu-desktop`
    
- **Delete:** `sudo apt remove xubuntu-desktop xfce4 && sudo apt autoremove`
    

#### 3. Cinnamon (Linux Mint default)

A traditional, highly polished desktop that balances modern aesthetics with older navigation paradigms.

- **Install:** `sudo apt install cinnamon-desktop-environment`
    
- **Delete:** `sudo apt remove cinnamon-desktop-environment cinnamon-core && sudo apt autoremove`
    

#### 4. MATE (Ubuntu MATE)

A continuation of the classic GNOME 2 desktop. Stable, lightweight, and retro.

- **Install:** `sudo apt install ubuntu-mate-desktop`
    
- **Delete:** `sudo apt remove ubuntu-mate-desktop mate-desktop-environment && sudo apt autoremove`
    

#### 5. LXQt (Lubuntu)

The absolute lightest modern environment available for Ubuntu, focused on saving RAM.

- **Install:** `sudo apt install lubuntu-desktop`
    
- **Delete:** `sudo apt remove lubuntu-desktop lxqt-core && sudo apt autoremove`
    

#### 6. Budgie (Ubuntu Budgie)

A sleek, modern environment that uses GNOME technologies but provides a more traditional layout.

- **Install:** `sudo apt install ubuntu-budgie-desktop`
    
- **Delete:** `sudo apt remove ubuntu-budgie-desktop budgie-desktop && sudo apt autoremove`

---
# 7. How to install `.deb` file?

- Go to file directory and type following command:

```bash
sudo apt install ./filename.deb
```
