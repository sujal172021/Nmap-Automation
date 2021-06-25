# Nmap-Automation

# summary

The main goal for this script is to automate the process of enumeration & recon that is run every time, and instead focus our attention on real pentesting.

This will ensure two things:
1. Automate nmap scans.
2. Always have some recon running in the background.

Once initial ports are found 'in 5-10 seconds', we can start manually looking into those ports, and let the rest run in the background with no interaction from our side whatsoever.

# Features

Scans
1. Network : Shows all live hosts in the host's network (~15 seconds)
2. Port : Shows all open ports (~15 seconds)
3. Script : Runs a script scan on found ports (~5 minutes)
4. Full : Runs a full range port scan, then runs a thorough scan on new ports (~5-10 minutes)
5. UDP : Runs a UDP scan "requires sudo" (~5 minutes)
6. Vulns : Runs CVE scan and nmap Vulns scan on all found ports (~5-15 minutes)
7. Recon : Suggests recon commands, then prompts to automatically run them
8. All : Runs all the scans (~20-30 minutes)
Note: This is a reconnaissance tool, and it does not perform any exploitation.

# Automatic Recon
With the recon option, nmapAutomator will automatically recommend and run the best recon tools for each found port.
If a recommended tool is missing from your machine, nmapAutomator will suggest how to install it.

# Runs on any shell
nmapAutomator is 100% POSIX compatible, so it can run on any sh shell, and on any unix-based machine (even a 10 YO router!), which makes nmapAutomator ideal for lateral movement recon.

If you want to run nmapAutomator on a remote machine, simply download a static nmap binary from this link, or with static-get, and transfer it to the remote machine. You can then use -s/--static-nmap to specify the path to the static nmap binary.

# Remote Mode (Beta)
With the -r/--remote flag nmapAutomator will run in Remote Mode, which is designed to run using POSIX shell commands only, without relying on any external tools.
Remote Mode is still under development. Only following scans currently work with -r:

 Network Scan (currently ping only)
 Port Scan
 Full Scan
 UDP Scan
 Recon Scan
 
# Output
nmapAutomator saves the output of each type of scan is saved into a separate file, under the output directory.
The entire script output is also saved, which you can view with less -r outputDir/nmapAutomator_host_type.txt, or you can simply cat it.
