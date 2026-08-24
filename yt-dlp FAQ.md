# Why need javascript runtime?

`yt-dlp` needs a JavaScript runtime (like Node.js) primarily to bypass **anti-bot protection** and **dynamically decrypt video URLs**.
Video platforms like YouTube don't want automated scripts downloading their content. To prevent this, they constantly change the way video streams are delivered. A JavaScript runtime acts as a weapon in this arms race.
Here is exactly why `yt-dlp` relies on it:
### 1. Decrypting the "n" Parameter (YouTube)

When you request a video on YouTube, the server sends back a scrambled stream URL. To unscramble it, YouTube's web player runs a complex, obfuscated JavaScript function to generate a specific token known as the **"n" parameter**.
- Because YouTube changes this JavaScript code frequently, hardcoding a fix in Python (the language `yt-dlp` is written in) would break every few days.    
- Instead of constantly rewriting Python code, `yt-dlp` can simply pass YouTube's obfuscated code into a JavaScript runtime to execute it exactly as a web browser would, instantly getting the correct decryption key.
### 2. Solving Signature Ciphers (The "s" Parameter)

Similar to the "n" parameter, copyrighted or age-restricted videos often use a signature cipher (the `s` parameter). The mathematical operations required to unlock the signature are hidden inside the site's JavaScript. Running that script directly via Node.js guarantees that `yt-dlp` gets the exact required output to unlock the video.
### 3. Bypassing Anti-Scraping Challenges

Many websites supported by `yt-dlp` sit behind protection services like Cloudflare. When you visit these sites, they run a background JavaScript challenge to verify you are a real browser and not a scraping tool. `yt-dlp` uses a JavaScript runtime to silently solve these math puzzles and pass the bot checks.  
### 4. Handling Complex Extractors

While `yt-dlp` actually has a very basic, built-in JavaScript interpreter written in Python, it is limited. When platforms use modern, highly complex JavaScript features (like WebAssembly or advanced minification), `yt-dlp`'s internal interpreter fails. A dedicated runtime like Node.js can process anything the site throws at it.  

> **Note:** For many standard videos, `yt-dlp` works fine without an external JS runtime by using its own internal tools. However, installing **Node.js** alongside `yt-dlp` is highly recommended, as it acts as a failsafe when extractors encounter heavily obfuscated code.

## Installing Node JS

The good news is that you do not need to link or configure Node.js inside `yt-dlp`. As long as Node.js is installed on your computer and added to your system's "PATH" (which allows programs to find it), `yt-dlp` will automatically detect and use it when needed.
Here is how to get it set up:
**1.Install Node.js for your Operating System:**The exact method depends on your device.
**Windows and macOS:**
1. Go to the official website: [nodejs.org](https://nodejs.org/).    
2. Download the **LTS (Long Term Support)** installer.    
3. Run the installer. **Crucial detail:** Make sure the **"Add to PATH"** option is checked during the installation process (it usually is by default).
**Linux (Debian/Ubuntu):**
Open your terminal and run:
`sudo apt update && sudo apt install nodejs`
**2.Verify the installation:**Ensure your system recognizes the command.
You must open a **new** Terminal or Command Prompt window (so it loads the updated PATH variables). Type the following command and press Enter:
`node -v`
If it successfully returns a version number (for example, `v20.11.0`), your installation was successful.
**3.Run yt-dlp normally:**Let the tool do the rest.
You are done! You don't need to add any special flags or commands when using `yt-dlp`. Whenever it encounters heavy obfuscation or anti-bot checks, it will automatically call upon Node.js in the background to solve them.

---
1. **How to solve** `WARNING: [youtube] No supported JavaScript runtime could be found. Only deno is enabled by default; to use another runtime add  --js-runtimes RUNTIME[:PATH]  to your command/config. YouTube extraction without a JS runtime has been deprecated, and some formats may be missing. See  https://github.com/yt-dlp/yt-dlp/wiki/EJS  for details on installing one` **issue**?

#### Solution:

This warning is popping up because of a recent security update in `yt-dlp`.
Because JavaScript runtimes (like Node.js) can potentially interact with your computer's file system, the `yt-dlp` developers decided it was dangerous to let the tool run scripts through Node.js automatically. Malicious websites could theoretically use it to run harmful code on your machine.
To protect users, `yt-dlp` now only allows **Deno** by default (because Deno runs in a strict, isolated sandbox). Since you have Node.js instead, you have to explicitly give `yt-dlp` permission to use it.
Here are the two ways to fix this:
### Option 1: The Quick Fix (Command Line)

If you just want to download a video right now, you need to add a special flag to your command to authorize Node.js.
Add `--js-runtimes nodejs` to your usual command. It should look like this:  
```bash
yt-dlp --js-runtimes nodejs [YOUR_VIDEO_URL]
```
### Option 2: The Permanent Fix (Configuration File)

Typing that flag every time is annoying. You can add it to your `yt-dlp` configuration file so it applies automatically to every download.
1. **Find or create your config file:**      
    - **Windows:** Open File Explorer and type `%APPDATA%` in the address bar. Create a folder named `yt-dlp`. Inside that folder, create a standard text file named `config` (make sure it doesn't have a `.txt` extension at the end).        
    - **macOS / Linux:** Open your terminal and create a config file at `~/.config/yt-dlp/config`.        
2. **Edit the file:**    
    Open the `config` file with any basic text editor (like Notepad or TextEdit).    
3. **Add the flag:**
```bash
--js-runtimes nodejs
```
4. **Save and close.**
Now, when you run standard `yt-dlp [URL]` commands, it will automatically read that file, authorize Node.js, and process the YouTube video without throwing that warning.

---
1. **How to use cookies?**

#### Solution:

Assuming you mean **`yt-dlp`** (the popular video downloader), you actually don't need to manually extract cookies in most cases. `yt-dlp` has a built-in feature to read them directly from your browser's local database on both Windows and Linux.

  

Here is exactly how to do it, along with a fallback method if the built-in way fails.

  

## Method 1: The Built-In Way (Recommended)

You can tell `yt-dlp` to automatically pull your login session from your installed browser using the `--cookies-from-browser` flag.

  

**Basic Syntax:**

  

Bash

```
yt-dlp --cookies-from-browser BROWSER "VIDEO_URL"
```

**Supported Browsers:** `chrome`, `chromium`, `edge`, `firefox`, `brave`, `opera`, `vivaldi`, `safari`.

  

### Examples

If you are logged into YouTube (or another site) on **Firefox**:

  

Bash

```
yt-dlp --cookies-from-browser firefox "https://www.youtube.com/watch?v=..."
```

If you use **Chrome**:

  

Bash

```
yt-dlp --cookies-from-browser chrome "https://www.youtube.com/watch?v=..."
```

> **Important OS-Specific Notes:**
> 
>   
> 
> - **Windows:** Chrome, Edge, and Brave lock their cookie databases while open. You will likely need to **close the browser completely** before running the `yt-dlp` command, otherwise you will get a "database is locked" error.
>     
>       
>     
> - **Linux (Snap/Flatpak):** If your browser was installed via Snap or Flatpak (common on Ubuntu/Mint), `yt-dlp` might not find the default path. You can pass the explicit path to the browser's profile folder like this:
>     
>     `yt-dlp --cookies-from-browser chrome:/home/user/snap/chromium/common/chromium/Default`
>     
>       
>     

## Method 2: The "cookies.txt" File (Fallback)

If `yt-dlp` cannot read your browser directly (which happens with certain Linux keyrings or strict antivirus software on Windows), you can export a traditional cookie file.

  

1. **Install a Cookie Exporter Extension:**
    
      
    - Install **"Get cookies.txt LOCALLY"** (available for Chrome/Edge/Brave and Firefox). _Note: Ensure it's a reputable one that doesn't send your cookies to a third-party server._
        
          
        
2. **Export the Cookies:**
    
      
    - Go to the website you want to download from (e.g., youtube.com).
        
          
        
    - Click the extension icon and export the cookies for that site.
        
          
        
    - Save the file as `cookies.txt` in the same folder where you are running `yt-dlp`.
        
          
        
3. **Run yt-dlp with the file:**
    
    Instead of the browser flag, use the `--cookies` flag pointing to your file:
    
    Bash
    
    ```
    yt-dlp --cookies cookies.txt "https://www.youtube.com/watch?v=..."
    ```