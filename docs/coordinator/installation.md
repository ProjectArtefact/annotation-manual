# Installation

> **This page is for the study coordinator (Amey).** Clinicians do not install anything. Once CVAT is running, clinicians connect via SSH tunnel — see [Clinician Workflow](../clinicians/clinician-workflow.md).

These instructions are for installing CVAT on the **dedicated university PC running Ubuntu Linux**. This is a one-time process.

---

## Before You Start

Make sure you have:
- [ ] At least **50 GB** of free disk space on the university PC
- [ ] An internet connection on the university PC (needed only during installation)
- [ ] SSH access to the university PC (or physical access to a keyboard and monitor)
- [ ] The IP address of the university PC (run `hostname -I` in a terminal to find it)

---

## Step 1 — Install Docker

Open a terminal on the university PC and run each block of commands below. Copy the full block, paste it in, and press Enter.

```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

```bash
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Allow Docker to run without `sudo` (then log out and back in for this to take effect):

```bash
sudo usermod -aG docker $USER
```

After logging back in, confirm Docker works:

```bash
docker run hello-world
```

You should see "Hello from Docker!" — if so, Docker is working correctly.

---

## Step 2 — Install Git

```bash
sudo apt-get install -y git
```

---

## Step 3 — Download CVAT

```bash
git clone https://github.com/cvat-ai/cvat
cd cvat
```

---

## Step 4 — Start CVAT

```bash
docker compose up -d
```

This downloads all required components and starts CVAT. **It takes 5–15 minutes** the first time. You will see a lot of text — this is normal. When it finishes and the terminal prompt returns, CVAT is running.

Check that all components started correctly:

```bash
docker compose ps
```

All services should show `running` or `Up`.

---

## Step 5 — Create Your Admin Account

```bash
docker exec -it cvat_server bash -ic 'python3 ~/manage.py createsuperuser'
```

You will be asked for:
- **Username** — choose something you will remember (e.g. `amey`)
- **Email address** — your university email
- **Password** — choose a strong password

Write these down. This is the main account you use to manage CVAT.

---

## Step 6 — Verify CVAT Is Working

Open **Google Chrome** on the university PC and go to:

```
http://localhost:8080
```

Log in with the username and password you just created. You should see the CVAT dashboard.

---

## Step 7 — Find the University PC's IP Address

You will need to give this address to clinicians so they can connect via SSH.

```bash
hostname -I
```

The first address shown (e.g. `130.251.10.25`) is the IP address. Write it down and include it in the connection instructions you send to clinicians.

---

## Step 8 — Make Sure SSH Is Enabled

Check if SSH is already running:

```bash
sudo systemctl status ssh
```

If it says `active (running)`, SSH is already enabled — you can skip to Step 9.

If it is not running:

```bash
sudo apt-get install -y openssh-server
sudo systemctl enable ssh
sudo systemctl start ssh
```

---

## Step 9 — Verify a Clinician Can Connect

Ask a clinician to follow the [Clinician Workflow](../clinicians/clinician-workflow.md#connecting-for-the-first-time-mac) connection guide using the IP address from Step 7 and their SSH credentials (which you create in [First Login and Setup](first-login-and-setup.md#step-2-create-ssh-accounts-for-each-clinician)).

---

## Stopping and Starting CVAT

To **stop** CVAT (e.g. for maintenance):
```bash
cd ~/cvat
docker compose down
```

To **start** CVAT again:
```bash
cd ~/cvat
docker compose up -d
```

> **After restarting:** If you have installed AI models (SAM + tracker), you will need to redeploy them — see [Installing AI Models](installing-ai-models.md#restarting-after-the-server-reboots).

---

## Keeping CVAT Updated

```bash
cd ~/cvat
docker compose down
git pull
docker compose pull
docker compose up -d
```

---

## Checking CVAT Is Healthy

Run this at any time to check all components are working:

```bash
docker exec -t cvat_server python manage.py health_check
```

All lines should end with `... working`.

---

## Next Step

- [First Login and Setup](first-login-and-setup.md) — create SSH and CVAT accounts for clinicians
- [Installing AI Models](installing-ai-models.md) — enable AI-assisted annotation tools
