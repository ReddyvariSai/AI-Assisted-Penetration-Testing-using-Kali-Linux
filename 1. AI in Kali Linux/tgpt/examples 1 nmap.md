```
┌──(sai㉿kalki)-[~]
└─$ tgpt -i
Interactive mode started. Press Ctrl + C or type exit to quit.
```

╭─ You

╰─> hi

╭─ Bot

Hello! 👋 How can I help you today?

---

╭─ You

╰─> tell me how can i use nmap

╭─ Bot
## Quick‑Start Guide to Nmap

> Nmap (“Network Mapper”) is an open‑source network discovery & security‑auditing tool.
> **Always run it on networks you own or on which you have explicit permission.**
> Unauthorized scanning can be illegal and is often considered hostile behavior.

---

### 1.  Install Nmap

| OS | Command |
|----|---------|
| **Ubuntu/Debian** | sudo apt update && sudo apt install nmap |
| **Fedora/RedHat** | sudo dnf install nmap |
| **Arch/Linux** | sudo pacman -S nmap |
| **Windows** | Download the installer [here](https://nmap.org/download.html) and run it. (You can also use the WSL or C
ygwin options.) |
| **macOS (Homebrew)** | brew install nmap |
| **macOS (macPorts)** | sudo port install nmap |

> On most Linux distros you'll install it from the default repo.
> After installation, just type nmap -v to confirm it's ready.

---

### 2.  Basic Scanning

#### 2.1 Ping Scan (Host Discovery)
```bash
# Find live hosts on a subnet
nmap -sn 192.168.1.0/24
```
* -sn: “Ping scan” (no port scan, just check if a host is up)

#### 2.2 Port Scan (TCP SYN Scan – “Stealth”)
```bash
# Scan the 100 most common ports
nmap -sS -T4 192.168.1.10
```
* -sS: TCP SYN (half‑open) scan.
* -T4: Aggressive timing (fast). Use -T5 for very aggressive, but be careful not to alert IDS.

#### 2.3 Scan a Full TCP/UDP Range
```bash
# All 65535 ports
nmap -p- -sS -T4 192.168.1.10
```
* -p-: Scan *all* ports.

---

### 3.  OS & Version Detection

```bash
# OS fingerprint + service versions + default scripts
nmap -A 192.168.1.10
```
* -A: Enables OS detection (-O), version detection (-sV), script scanning (--script=default), and traceroute.

> **Tip:** On networks with strong firewalls this may be noisy. Use with care.

---

### 4.  NSE (Nmap Scripting Engine)

#### Simple Script Run
```bash
# Test for default credentials
nmap --script=default -p 80 192.168.1.10
```

#### Using Popular Script Collections
```bash
# Enumerate SMB shares
nmap --script=smb-enum-shares.nse -p 445 192.168.1.10
```

#### Running All Scripts (Caution!)
```bash
# Very verbose, may take a long time
nmap --script=all -p 1-65535 192.168.1.10
```

> **Rule of thumb:** If you’re uncertain, start with --script=default or a targeted collection.

---

### 5.  Output Formats

| Format | Flag | Use‑case |
|--------|------|-----------|
| Normal | -oN file.txt | Quick human‑readable |
| XML | -oX file.xml | Import into GUIs (Zenmap, Nmap‑tools) |
| Greppable | -oG file.txt | Easy grep filtering |
| JSON | -oJ file.json | API consumption, automation |

*You can specify multiple at once: -oN out.txt -oX out.xml.*

---

### 6.  Advanced Options

| Option | Description | Example |
|--------|-------------|---------|
| -iL file.txt | Input list of targets | nmap -iL hosts.txt -sV |
| -sU | UDP scan | nmap -sU 192.168.1.10 |
| -p 1-1000,8080,8443 | Custom port ranges | |
| -Pn | Treat all hosts as online (skip ping) | |
| -v, -vv, -vvv | Verbose levels | nmap -v 192.168.1.10 |
| --max-retries 1 | Fewer attempts for faster scans | |
| -e eth0 | Bind to a network interface | |
| --reason | Show why a port was filtered | |

> **Tip:** Combine -T0 to -T5 to choose speed vs stealth.
> -T0 is the safest but slowest; -T5 is fastest and most likely to get blocked.

---

### 7.  Sample Scan Workflows

#### 7.1 Recon on a New Network
```bash
# Discover hosts
nmap -sn 10.10.10.0/24

# Full TCP scan of live hosts
nmap -sS -T4 -p- -oN scans/initial_full_tcp.txt $(grep -v '^#' live_hosts.txt | awk '{print $5}')

# OS & version detection on key sub‑net
nmap -A 10.10.10.0/24 -oN scans/os_and_version_scan.txt
```

#### 7.2 Targeted Pen‑Test
```bash





---

**Support Pollinations.AI:**

---

🌸 **Ad** 🌸
Powered by Pollinations.AI free text APIs. [Support our mission](https://pollinations.ai/redirect/kofi) to keep AI accessible for everyone.

╭─ You
╰─>
