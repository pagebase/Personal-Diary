Setting up Ubuntu for gaming has become incredibly streamlined over the past few years, thanks to tools like Steam's Proton and a robust open-source community. Here is a comprehensive guide to turning your Ubuntu system into a capable gaming machine.

  

## 1. Update Your System

Before installing anything, ensure your system and its packages are up to date. Open your terminal (`Ctrl + Alt + T`) and run:

  

Bash

```
sudo apt update && sudo apt upgrade -y
```

## 2. Install the Right Graphics Drivers

Having the correct, up-to-date graphics drivers is the single most important step for gaming performance.

  

- **For NVIDIA GPUs:** You _must_ install the proprietary drivers. Open the **"Software & Updates"** app, navigate to the **"Additional Drivers"** tab, and select the latest tested proprietary NVIDIA driver. Click "Apply Changes" and reboot your system. Alternatively, you can use the terminal:
    
      
    
    Bash
    
    ```
    sudo apt install nvidia-driver-525
    ```
    
    _(Note: Replace "525" with the latest version available for your card)_.
    
      
    
- **For AMD and Intel GPUs:** You're largely good to go out of the box! The open-source `Mesa` drivers are pre-installed in the Linux kernel and provide excellent performance. You may just need to install Vulkan support:
    
      
    
    Bash
    
    ```
    sudo apt install mesa-vulkan-drivers
    ```
    

## 3. Install Steam and Enable Proton

Valve’s Steam is the easiest way to game on Linux, and their compatibility layer, **Proton**, allows you to run thousands of Windows games seamlessly.

  

1. **Install Steam:** You can install it via the Ubuntu App Center (look for the Debian package, not the Snap version for the best hardware integration) or via the terminal:
    
      
    
    Bash
    
    ```
    sudo apt install steam
    ```
    
2. **Enable Proton:** Open Steam, go to **Steam > Settings > Compatibility**.
    
      
    
3. Check the box for **"Enable Steam Play for all other titles"**.
    
      
    
4. Select a Proton version from the dropdown (usually, **Proton Experimental** or the latest stable release is best). Restart Steam.
    
      
    

You can now download and play most Windows games right from your Steam library. You can check the community site **ProtonDB** to see how well specific games run.

  

## 4. Install Alternative Launchers

If you have games on platforms like the Epic Games Store, GOG, or Amazon Games, you won't be able to install their native clients directly. Instead, you use community-built launchers that manage the Wine/Proton compatibility layers for you:

  

- **Heroic Games Launcher:** The best choice for Epic Games and GOG libraries. It has a beautiful interface and handles everything seamlessly.
    
      
    
- **Lutris:** A massive library manager that can install games from almost any source (Origin, Ubisoft Connect, standalone Windows installers, emulators) using community-written install scripts.
    
      
    

Both are easily installed as Flatpaks from **Flathub** or through the Ubuntu App Center.

  

## 5. Performance Tweaks (Optional but Recommended)

For an extra boost, you can install **GameMode**, a daemon by Feral Interactive that optimizes system performance on demand (adjusting CPU governor, I/O priority, etc.) when a game is running.

  

Bash

```
sudo apt install gamemode
```

Once installed, you can enable it for specific games in Steam by right-clicking the game, selecting **Properties**, and adding this to the Launch Options:

`gamemoderun %command%`

  

Lutris and Heroic often have toggle switches in their settings to enable GameMode globally.

---
I see the error in your screenshot, `image_d3e21c.png`. The `Unable to locate package` message means that version 525 of the NVIDIA driver is not available in your currently configured software repositories. This usually happens because your specific version of Ubuntu has moved on to a newer driver version (like 535 or 550) and dropped the older one.

  

Here is how you can find and install the correct driver for your exact setup.

  

## 1. Identify Available Drivers

Instead of guessing the version number, Ubuntu has a built-in tool that will check your hardware and tell you exactly which drivers are available for your card. Run this command in your terminal:

  

Bash

```
ubuntu-drivers devices
```

> **Note:** Look at the output for a line that ends with the word `recommended`. It will usually look something like `driver : nvidia-driver-535 - distro non-free recommended`.
> 
>   

## 2. Install the Recommended Driver

You can either install the specific package name you found in the previous step, or you can let Ubuntu automatically install the recommended version for you.

  

To automatically install the recommended driver, run:

  

Bash

```
sudo ubuntu-drivers install
```

If you prefer to manually specify the version based on what you found (for example, if version 535 was the recommended one), run:

  

Bash

```
sudo apt install nvidia-driver-535
```

Once the installation finishes, make sure to reboot your computer so the new drivers can take effect.

  

## 3. The Graphical Alternative

If the terminal continues to give you trouble, the graphical interface is often the most foolproof method to get this done:

  

- Press the `Super` (Windows) key and search for **Software & Updates**.
    
      
    
- Open the application and navigate to the **Additional Drivers** tab.
    
      
    
- Wait a moment for it to scan your hardware.
    
      
    
- Select the topmost NVIDIA proprietary, tested driver from the list.
    
      
    
- Click **Apply Changes**, wait for the installation to finish, and reboot your PC.
    
      
    

What specific NVIDIA graphics card do you have installed in your system?