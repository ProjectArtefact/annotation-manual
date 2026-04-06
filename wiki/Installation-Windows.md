# Installation — Windows 10 / 11

CVAT on Windows runs inside the Windows Subsystem for Linux 2 (WSL2) with Docker Desktop. This is the supported approach for Windows.

> **Who should do this:** The server administrator. Annotators do not need to install anything.

---

## Step 1 — Install WSL2

1. Open **PowerShell as Administrator** (right-click the Start menu → "Windows PowerShell (Admin)").
2. Run:

```powershell
wsl --install
```

3. Restart your computer when prompted.
4. After restarting, a terminal will open and ask you to create a Linux username and password. Choose something you will remember.

> If you already have WSL installed, ensure you are using WSL2 by running `wsl --set-default-version 2`.

---

## Step 2 — Install Docker Desktop

1. Download [Docker Desktop for Windows](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe).
2. Double-click the installer and follow the prompts. Accept the default options.
3. When installation finishes, start Docker Desktop from the Start menu.
4. In Docker Desktop, go to **Settings → Resources → WSL Integration** and enable integration for your Linux distribution (e.g. Ubuntu).
5. Click **Apply & Restart**.

---

## Step 3 — Install Git for Windows

Download and install [Git for Windows](https://git-scm.com/download/win). Accept all default options during installation.

---

## Step 4 — Install Google Chrome

Download and install [Google Chrome](https://www.google.com/chrome/) if you do not already have it. CVAT only supports Chrome.

---

## Step 5 — Open Your Linux Terminal

From the Start menu, find and open the Linux distribution you installed (e.g. **Ubuntu**). A terminal window will appear.

All remaining commands should be run **inside this Linux terminal**.

---

## Step 6 — Download CVAT

```bash
git clone https://github.com/cvat-ai/cvat
cd cvat
```

---

## Step 7 — Configure the Server Address (if using across a network)

If annotators will connect from other computers, set the server's IP address. Replace `YOUR-IP-ADDRESS` with your Windows machine's local IP (find it by running `ipconfig` in Command Prompt and looking for "IPv4 Address"):

```bash
export CVAT_HOST=YOUR-IP-ADDRESS
```

---

## Step 8 — Start CVAT

```bash
docker compose up -d
```

The first run downloads Docker images and takes **5–15 minutes**. Once complete, check that all services are running:

```bash
docker compose ps
```

---

## Step 9 — Create an Administrator Account

```bash
docker exec -it cvat_server bash -ic 'python3 ~/manage.py createsuperuser'
```

Enter a username, email, and password when prompted.

---

## Step 10 — Open CVAT

Open Google Chrome and go to:

```
http://localhost:8080
```

Log in with the administrator credentials you just created.

---

## Stopping and Starting CVAT

In your Linux terminal, from the `cvat` directory:

```bash
# Stop
docker compose down

# Start again
docker compose up -d
```

---

## Troubleshooting Windows-Specific Issues

**Docker Desktop not starting:** Make sure virtualisation is enabled in your BIOS/UEFI settings. Look for "Intel VT-x" or "AMD-V".

**WSL integration not working:** In Docker Desktop go to Settings → Resources → WSL Integration and confirm your distribution is toggled on.

**Port 8080 already in use:** Another application may be using port 8080. Check with `netstat -an | findstr 8080` in Command Prompt.

---

## Next Steps

- [First Login and Setup](First-Login-and-Setup)
- [Installing AI Models (Nuclio + SAM)](Installing-AI-Models)
