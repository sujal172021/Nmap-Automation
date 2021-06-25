# Nmap-Automation
Summary
The main goal for this script is to automate the process of enumeration & recon that is run every time, and instead focus our attention on real pentesting.

This will ensure two things:

Automate nmap scans.
Always have some recon running in the background.
Once initial ports are found 'in 5-10 seconds', we can start manually looking into those ports, and let the rest run in the background with no interaction from our side whatsoever.

Features
Scans
Network : Shows all live hosts in the host's network (~15 seconds)
Port : Shows all open ports (~15 seconds)
Script : Runs a script scan on found ports (~5 minutes)
Full : Runs a full range port scan, then runs a thorough scan on new ports (~5-10 minutes)
UDP : Runs a UDP scan "requires sudo" (~5 minutes)
Vulns : Runs CVE scan and nmap Vulns scan on all found ports (~5-15 minutes)
Recon : Suggests recon commands, then prompts to automatically run them
All : Runs all the scans (~20-30 minutes)
Note: This is a reconnaissance tool, and it does not perform any exploitation.

Automatic Recon
With the recon option, nmapAutomator will automatically recommend and run the best recon tools for each found port.
If a recommended tool is missing from your machine, nmapAutomator will suggest how to install it.

Runs on any shell
nmapAutomator is 100% POSIX compatible, so it can run on any sh shell, and on any unix-based machine (even a 10 YO router!), which makes nmapAutomator ideal for lateral movement recon.

If you want to run nmapAutomator on a remote machine, simply download a static nmap binary from this link, or with static-get, and transfer it to the remote machine. You can then use -s/--static-nmap to specify the path to the static nmap binary.

Remote Mode (Beta)
With the -r/--remote flag nmapAutomator will run in Remote Mode, which is designed to run using POSIX shell commands only, without relying on any external tools.
Remote Mode is still under development. Only following scans currently work with -r:

 Network Scan (currently ping only)
 Port Scan
 Full Scan
 UDP Scan
 Recon Scan
Output
nmapAutomator saves the output of each type of scan is saved into a separate file, under the output directory.
The entire script output is also saved, which you can view with less -r outputDir/nmapAutomator_host_type.txt, or you can simply cat it.

Requirements:
ffuf, which we can install with:

sudo apt update
sudo apt install ffuf -y
Or Gobuster 'v3.0 or higher', which we can install with:

sudo apt update
sudo apt install gobuster -y
Other recon tools used within the script include:

nmap Vulners	sslscan	nikto	joomscan	wpscan
droopescan	smbmap	enum4linux	dnsrecon	odat
smtp-user-enum	snmp-check	snmpwalk	ldapsearch	
Most of these should be installed by default in Parrot OS and Kali Linux.
If any recon recommended tools are found to be missing, they will be automatically omitted, and the user will be notified.

Installation:
git clone https://github.com/21y4d/nmapAutomator.git
sudo ln -s $(pwd)/nmapAutomator/nmapAutomator.sh /usr/local/bin/
Usage:
./nmapAutomator.sh -h
Usage: nmapAutomator.sh -H/--host <TARGET-IP> -t/--type <TYPE>
Optional: [-r/--remote <REMOTE MODE>] [-d/--dns <DNS SERVER>] [-o/--output <OUTPUT DIRECTORY>] [-s/--static-nmap <STATIC NMAP PATH>]

Scan Types:
	Network : Shows all live hosts in the host's network (~15 seconds)
	Port    : Shows all open ports (~15 seconds)
	Script  : Runs a script scan on found ports (~5 minutes)
	Full    : Runs a full range port scan, then runs a thorough scan on new ports (~5-10 minutes)
	UDP     : Runs a UDP scan "requires sudo" (~5 minutes)
	Vulns   : Runs CVE scan and nmap Vulns scan on all found ports (~5-15 minutes)
	Recon   : Suggests recon commands, then prompts to automatically run them
	All     : Runs all the scans (~20-30 minutes)
Example scans:

./nmapAutomator.sh --host 10.1.1.1 --type All
./nmapAutomator.sh -H 10.1.1.1 -t Basic
./nmapAutomator.sh -H academy.htb -t Recon -d 1.1.1.1
./nmapAutomator.sh -H 10.10.10.10 -t network -s ./nmap
