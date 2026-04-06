# Installation — macOS

These instructions cover installation on macOS (Intel and Apple Silicon).

> **Who should do this:** The server administrator. Annotators do not need to install anything.

---

## Step 1 — Install Docker Desktop for Mac

1. Go to [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/) and download the correct version for your Mac:
   - **Intel Mac:** choose "Mac with Intel chip"
   - **Apple Silicon (M1/M2/M3/M4):** choose "Mac with Apple Silicon"
2. Open the downloaded `.dmg` file and drag Docker to your Applications folder.
3. Launch Docker from the Applications folder. You will see the Docker whale icon in the menu bar.
4. Wait until the icon shows Docker is running (the animation stops).

---

## Step 2 — Install Git

Open the **Terminal** app (Applications → Utilities → Terminal).

Check if Git is already installed:

```bash
git --version
```

If macOS prompts you to install command-line developer tools, click **Install** and follow the prompts.

Alternatively, install Git via Homebrew:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
brew install git
```

---

## Step 3 — Install Google Chrome

Download and install [Google Chrome](https://www.google.com/chrome/) if you do not already have it.

---

## Step 4 — Download CVAT

In the Terminal:

```bash
git clone https://github.com/cvat-ai/cvat
cd cvat
```

---

## Step 5 — Configure the Server Address (if sharing across a network)

Find your Mac's local IP address: go to **System Settings → Network → Wi-Fi (or Ethernet) → Details** and note the IP address.

Then in Terminal:

```bash
export CVAT_HOST=YOUR-IP-ADDRESS
```

---

## Step 6 — Start CVAT

```bash
docker compose up -d
```

The first run downloads all Docker images and takes **5–15 minutes**. Check the status with:

```bash
docker compose ps
```

All services should show `Up` or `running`.

---

## Step 7 — Create an Administrator Account

```bash
docker exec -it cvat_server bash -ic 'python3 ~/manage.py createsuperuser'
```

Enter a username, email address, and password.

---

## Step 8 — Open CVAT

Open Google Chrome and go to:

```
http://localhost:8080
```

Log in with your administrator credentials.

---

## Apple Silicon (M1/M2/M3/M4) Notes

CVAT works on Apple Silicon through Docker Desktop's Rosetta 2 emulation layer. Performance is generally good for the main CVAT interface. However:

- AI models that run as serverless functions (SAM, tracking) may have compatibility issues on Apple Silicon. If you encounter problems, consider using an Ubuntu server for AI-assisted annotation and connecting annotators to it remotely.
- In Docker Desktop settings, enabling **"Use Rosetta for x86/amd64 emulation on Apple Silicon"** (under Features in Development) can improve compatibility.

---

## Stopping and Starting CVAT

```bash
# Stop (from inside the cvat directory)
docker compose down

# Start again
docker compose up -d
```

---

## Next Steps

- [First Login and Setup](First-Login-and-Setup)
- [Installing AI Models (Nuclio + SAM)](Installing-AI-Models)
