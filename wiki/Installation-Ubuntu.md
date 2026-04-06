# Installation — Ubuntu (Recommended)

These instructions are for **Ubuntu 20.04 or 22.04** (64-bit, x86). This is the recommended platform for running CVAT.

> **Who should do this:** The server administrator. Annotators do not need to install anything — they just open Google Chrome and navigate to the server address.

---

## Step 1 — Install Docker

Open a terminal and run the following commands one block at a time. Copy each block in full, paste it into the terminal, and press Enter.

```bash
# Add Docker's official GPG key
sudo apt-get update
sudo apt-get install -y ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

```bash
# Add the Docker repository
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

```bash
# Install Docker
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

### Allow running Docker without `sudo` (recommended)

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```

**Log out and log back in** (or reboot) for this change to take effect. You can verify it worked by running:

```bash
docker run hello-world
```

You should see a message that starts with "Hello from Docker!".

---

## Step 2 — Install Git

```bash
sudo apt-get install -y git
```

---

## Step 3 — Install Google Chrome

```bash
sudo curl https://dl-ssl.google.com/linux/linux_signing_key.pub -o /etc/apt/trusted.gpg.d/google.asc
sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
sudo apt-get update
sudo apt-get install -y google-chrome-stable
```

---

## Step 4 — Download CVAT

Clone the CVAT repository into a directory of your choice. The home directory is a sensible location.

```bash
git clone https://github.com/cvat-ai/cvat
cd cvat
```

---

## Step 5 — Configure the Server Address

If annotators will connect from **other machines on the network**, set the server's IP address or hostname. Replace `YOUR-IP-ADDRESS` with the actual IP (e.g. `192.168.1.50`):

```bash
export CVAT_HOST=YOUR-IP-ADDRESS
```

If you are only using CVAT on the same machine it is installed on, you can skip this step.

> **Tip:** To find your server's IP address, run `ip addr show` and look for the `inet` line under your network interface (usually `eth0` or `ens3`).

---

## Step 6 — Start CVAT

This command downloads all required Docker images and starts CVAT. The first run takes **5–15 minutes** depending on your internet speed.

```bash
docker compose up -d
```

Once complete, you will see output confirming the containers have started. You can check their status at any time with:

```bash
docker compose ps
```

All services should show a status of `Up` or `running`.

---

## Step 7 — Create an Administrator Account

Run this command to create the first admin (superuser) account. You will be prompted to choose a username, email address, and password.

```bash
docker exec -it cvat_server bash -ic 'python3 ~/manage.py createsuperuser'
```

**Keep these credentials safe** — you will need them to log in and to create accounts for other users.

---

## Step 8 — Open CVAT

Open Google Chrome and go to:

```
http://localhost:8080
```

Or, if connecting from another machine on the network:

```
http://YOUR-IP-ADDRESS:8080
```

Log in with the administrator credentials you created in the previous step.

---

## Stopping and Starting CVAT

To stop CVAT (e.g. for maintenance):

```bash
cd ~/cvat
docker compose down
```

To start it again:

```bash
cd ~/cvat
docker compose up -d
```

---

## Keeping CVAT Updated

To update CVAT to the latest version:

```bash
cd ~/cvat
docker compose down
git pull
docker compose pull
docker compose up -d
```

---

## Next Steps

- [First Login and Setup](First-Login-and-Setup) — create user accounts for annotators
- [Installing AI Models (Nuclio + SAM)](Installing-AI-Models) — enable AI-assisted annotation *(do this before annotators begin)*
