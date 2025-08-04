
##  What I Wanted to Do

I wanted to:
- Scan a local IP to see which ports are open or filtered.
- Use Wireshark to capture the scan in action.
- Learn how network services respond (or don’t respond) to scans.
- Understand the meaning of filtered, open, and closed ports.


##  Step-by-Step Process

### 1. Checked My IP
I started with:
```bash
ip a
```

That showed my Kali machine's IP: 192.168.198.128

### 2. Tried Scanning Myself (Kali)
Out of curiosity, I scanned my own IP first:
```bash
sudo nmap -sS 192.168.198.128
```
Not much came up — no open ports. That made sense, since I wasn’t running any services that would respond to the scan.

### 3.Then Scanned My Router Instead
So I switched to scanning my router:
```bash
sudo nmap -sS 192.168.198.1
```
This was more interesting. Nmap said all ports were filtered, meaning the router just silently ignored the scan (probably a firewall doing its job). I saved this result to a text file:
```bash
sudo nmap -sS 192.168.198.1 -oN nmap_scan.txt
```

### 4. Watched the Scan in Wireshark
- While the scan was running, I opened Wireshark:
- Selected the interface: eth0
- Applied this filter:
```bash
ip.addr == 192.168.198.1
```
 I could see my machine sending TCP SYN packets to the router, but no replies came back. This visually confirmed that the ports were being filtered — exactly what Nmap said.

 ##  What I Learned
- Scanning your own machine usually shows nothing unless services are running.
- Devices like routers often block incoming packets silently (filtered).
- Nmap gives you the scan summary, but Wireshark helps you see it happen in real-time.
- Filtering, firewalls, and SYN scans all make more sense when you see the traffic for yourself.

## Final Outcome
From this, I was able to:
-Identify IP addresses and scan targets on my network.
-Perform a SYN scan with Nmap.
-Capture real-time network traffic using Wireshark.
-Understand how "filtered ports" behave during a scan.


 
