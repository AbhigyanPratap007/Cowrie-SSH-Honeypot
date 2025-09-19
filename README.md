# Cowrie SSH Honeypot Lab

**What:** Local Cowrie honeypot deployment to capture SSH brute-force attempts and attacker shell activity.  
**Stack:** Cowrie on Ubuntu VM (Python venv). No production exposure — lab only.

## What I did
- Deployed Cowrie on an Ubuntu VM and configured it to listen on port `2222`.
- Simulated brute-force logins and attacker commands (using `sshpass` loops).
- Collected structured events (`var/log/cowrie/cowrie.json`) and TTY session logs (`var/lib/cowrie/tty/`).
- Extracted results: **100+ failed login events**, top credential statistics, and TTY command captures for SOC reporting.

## Key files
- `logs/cowrie.json` — full JSON events (sample retained).
- `logs/tty_logs/` — TTY session files.
- `docs/setup_instructions.md` — commands for reproducing the lab.
- `docs/report.md` — short SOC-style analysis and findings.

## Quick reproduction
VM & Environment Setup
sudo apt update && sudo apt upgrade -y
sudo apt install git python3 python3-venv python3-pip libssl-dev libffi-dev build-essential virtualenv sshpass -y
Cowrie Installation
git clone https://github.com/cowrie/cowrie.git
cd cowrie
python3 -m venv cowrie-env
source cowrie-env/bin/activate
pip install --upgrade pip
pip install -r requirements.txt
cp etc/cowrie.cfg.dist etc/cowrie.cfg
nano etc/cowrie.cfg   # set listen_port = 2222
Run Cowrie
bin/cowrie start
bin/cowrie stop
tail -f var/log/cowrie/cowrie.json
Test Login (fake SSH session)
ssh root@localhost -p 2222
Simulated Attack Loop (Brute Force) - Basic
for u in root admin test user; do
  for p in 123456 password admin qwerty letmein; do
    sshpass -p "$p" ssh -o StrictHostKeyChecking=no -p 2222 "$u"@localhost "exit" 2>/dev/null || true
  done
done
Simulated Attack Loop (Brute Force) - Extended
for u in root admin test user dev; do
  for p in 123456 password admin qwerty letmein toor dragon shadow iloveyou default; do
    sshpass -p "$p" ssh -o StrictHostKeyChecking=no -p 2222 "$u"@localhost "exit" 2>/dev/null || true
  done
done
View Logs
tail -f var/log/cowrie/cowrie.json
ls var/lib/cowrie/tty/


