# Day 6: Cracking Passwords using Brute Force Tools

This session covers various tools for cracking passwords using brute force methods. Below are detailed instructions for using each tool.

## 1. Hashcat

Hashcat is a powerful GPU-accelerated password cracking tool that supports various hash types and attack modes.

### Installation
- On macOS: Install via Homebrew: `brew install hashcat`
- On Linux: `sudo apt install hashcat` (Ubuntu/Debian) or equivalent for your distro
- On Windows: Download from https://hashcat.net/hashcat/

### Basic Usage
1. Identify the hash type (e.g., MD5, SHA-256) using tools like `hashid` or online hash identifiers.
2. Prepare a wordlist (dictionary) file, e.g., `rockyou.txt`.
3. Run hashcat with the appropriate mode:

   ```
   hashcat -m <hash_type> -a 0 <hash_file> <wordlist>
   ```

   - `-m`: Hash mode (e.g., 0 for MD5, 100 for SHA-1, 1400 for SHA-256)
   - `-a 0`: Dictionary attack mode
   - `<hash_file>`: File containing the hash(es) to crack
   - `<wordlist>`: Path to your wordlist file

### Example
```
hashcat -m 0 -a 0 hashes.txt /usr/share/wordlists/rockyou.txt
```

### Advanced Options
- Brute force mode: `-a 3` (specify mask with `?a` for all chars)
- Hybrid attack: `-a 6` or `-a 7` (combine wordlist with masks)
- Use GPU: Automatically detected, use `-d` to specify device
- Show cracked passwords: `hashcat --show <hash_file>`

### Tips
- Use `--force` if you encounter driver issues
- Monitor temperature with `--status` and `--status-timer`
- For large wordlists, use `--remove` to remove cracked hashes from file

## 2. John The Ripper

John the Ripper is a fast password cracker that supports many hash types and is optimized for CPU cracking.

### Installation
- On macOS: `brew install john-jumbo`
- On Linux: `sudo apt install john` or compile from source for jumbo version
- On Windows: Download from https://www.openwall.com/john/

### Basic Usage
1. Prepare your hash file (e.g., from `/etc/shadow` or other sources).
2. Run John:

   ```
   john <hash_file>
   ```

   This uses default wordlist and rules.

### With Custom Wordlist
```
john --wordlist=<wordlist> <hash_file>
```

### Example
```
john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt
```

### Modes
- Single crack mode: `john --single <hash_file>` (uses login names, GECOS info)
- Incremental mode: `john --incremental <hash_file>` (brute force)
- External mode: `john --external=<mode> <hash_file>` (custom modes)

### Checking Progress and Results
- `john --show <hash_file>`: Show cracked passwords
- `john --status`: Show current status

### Tips
- Use `--fork=<N>` for multi-core systems
- Enable OpenMP with `--openmp` for better performance
- For GPU acceleration, use the OpenCL version if available

## 3. Crackstation Online

Crackstation is an online hash cracking service that uses massive computing power.

### Usage
1. Go to https://crackstation.net/
2. Enter your hash in the text box (supports multiple hashes, one per line)
3. Click "Crack Hashes"
4. Wait for results (can take from seconds to hours depending on hash complexity)

### Supported Hash Types
- MD5, SHA1, SHA256, SHA512
- MySQL, MSSQL, NTLM
- And many more

### Tips
- Use for quick checks or when local resources are insufficient
- Be aware of privacy concerns (hashes are sent to their servers)
- Free service with no registration required
- Results are cached, so repeated queries are fast

## 4. Hash Identifier

Hashidentifier is a tool to automatically identify the type of hash from a given hash string.

### Installation
- On Linux: `sudo apt install hash-identifier` or download from GitHub
- On macOS: Clone from GitHub and run with Python
- On Windows: Download and run with Python

### Usage
1. Run the tool: `hash-identifier` (or `python hash-identifier.py`)
2. Enter the hash when prompted
3. It will display possible hash types with confidence levels

### Example
```
$ hash-identifier
   #########################################################################
   #     __  __                     __           ______    _____           #
   #    /\ \/\ \                   /\ \         /\__  _\  /\  _ `\         #
   #    \ \ \_\ \     __      ____ \ \ \___     \/_/\ \/  \ \ \/\ \        #
   #     \ \  _  \  /'__`\   / ,__\ \ \  _ `\      \ \ \   \ \ \ \ \       #
   #      \ \ \ \ \/\ \_\ \_/\__, `\ \ \ \ \ \      \_\ \__ \ \ \_\ \      #
   #       \ \_\ \_\\ \___ \_\/\___/  \ \_\ \_\     /\_____\ \ \____/      #
   #        \/_/\/_/ \/_/ \/_/\/__/    \/_/\/_/     \/_____/  \/___/  v1.1 #
   #                                                             By Zion3R #
   #                                                    www.Blackploit.com #
   #                                                   Root@Blackploit.com #
   #########################################################################

   HASH: 5d41402abc4b2a76b9719d911017c592

   Possible Hashs:
   [+] MD5
   [+] Domain Cached Credentials - MD4(MD4(($pass)).(strtolower($username)))

   Least Possible Hashs:
   [+] RAdmin v2.x
   [+] NTLM
   [+] MD4
   [+] MD2
   [+] MD5(HMAC)
   [+] etc...
```

### Tips
- Useful before using cracking tools to determine the correct hash mode
- Supports many hash types including MD5, SHA1, SHA256, NTLM, etc.
- Can be used online at various hash identifier websites if preferred
- Always verify with multiple sources for accuracy

## General Tips for Password Cracking
- Always ensure you have permission to crack passwords
- Use strong wordlists like rockyou.txt, darkweb lists, or custom generated ones
- Understand hash types and use appropriate tools
- GPU acceleration (hashcat) is much faster than CPU for most hashes
- Rainbow tables can be faster for common hashes but require massive storage
- Legal and ethical considerations: Only crack passwords you own or have explicit permission for