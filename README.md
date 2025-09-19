# Cowrie-SSH-Honeypot
Cowrie SSH Honeypot Lab
📌 Overview

This project demonstrates the deployment of a Cowrie SSH honeypot on Ubuntu running in VMware. The honeypot was designed to simulate an exposed SSH server and capture attacker activity, including brute-force login attempts and command executions. The goal was to analyze attacker behavior, credentials used, and generate SOC-style reports to better understand real-world threats.

⚙️ Setup

Platform: VMware Workstation with Ubuntu VM

Honeypot Tool: Cowrie SSH Honeypot

Configuration:

Cowrie installed and configured to emulate an SSH server

Default services exposed to attract automated scanners and bots

Logging enabled to capture attacker commands and failed logins

🎯 Objectives

Deploy a controlled honeypot to attract brute-force attempts

Capture attacker behavior, including login attempts and commands

Analyze credential patterns used by attackers

Generate SOC-style reports on observed malicious activity

🔍 Methodology

Deployment: Installed Cowrie on an Ubuntu VM and configured it to accept SSH connections.

Attack Simulation: Exposed the VM to simulate internet-facing access.

Data Collection: Cowrie logged all incoming SSH connections, login attempts, and commands.

Analysis: Parsed log files to extract:

Common usernames and passwords attempted

Frequency of brute-force login attempts

Attacker interaction with the honeypot shell

📊 Results

Total SSH brute-force attempts recorded: 220+

Failed login events collected: 200+

Top credentials attempted:

root/123456

admin/password

test/test

Patterns observed:

Automated scripts attempting weak/default credentials

Attackers primarily targeting root/admin accounts

These findings demonstrate the constant nature of brute-force attacks on exposed SSH endpoints and emphasize the importance of strong authentication controls.

📄 Evidence & Reports

📑 Detailed log samples and screenshots are available in the COWRIE_HONEYPOT.pdf
.

✅ Key Takeaways

Honeypots provide real-world insights into attacker behavior with minimal risk.

Even a short deployment quickly attracts brute-force attempts.

Collected intelligence can feed into SOC workflows for detection and response.
