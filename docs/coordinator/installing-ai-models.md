# Installing AI Models

> **This is a one-time setup step** done by whoever installed CVAT. It only needs to be done once (and again if the server computer is restarted).
>
> If you are only annotating and someone else set up the server, skip this page. The AI tools will appear automatically in your annotation editor once they are set up.

---

## What This Sets Up

This guide installs two AI tools:

1. **Segment Anything Model (SAM)** — clinicians click on an object and the AI draws a precise mask around it instantly.
2. **TransT Tracker** — the AI follows an annotated object automatically across video frames.

Both are free and run entirely on your local server.

---

## Step 1 — Stop CVAT

If CVAT is already running, stop it first:

```bash
cd ~/cvat
docker compose down
```

---

## Step 2 — Restart CVAT with AI Support Enabled

Run this command to restart CVAT with the AI (serverless) components included. This replaces the usual startup command:

```bash
cd ~/cvat
docker compose -f docker-compose.yml \
               -f docker-compose.dev.yml \
               -f components/serverless/docker-compose.serverless.yml \
               up -d --build
```

This takes **10–20 minutes** the first time. When it finishes, check everything is running:

```bash
docker compose -f docker-compose.yml \
               -f docker-compose.dev.yml \
               -f components/serverless/docker-compose.serverless.yml ps
```

You should see a `nuclio` container listed with status `Up (healthy)`.

---

## Step 3 — Install the Model Deployment Tool (`nuctl`)

`nuctl` is a small tool used to install AI models onto the server. Run the commands for your operating system.

### Ubuntu / Linux or Windows (WSL terminal)

```bash
wget https://github.com/nuclio/nuclio/releases/download/1.13.0/nuctl-1.13.0-linux-amd64
chmod +x nuctl-1.13.0-linux-amd64
sudo mv nuctl-1.13.0-linux-amd64 /usr/local/bin/nuctl
```

### macOS

```bash
wget https://github.com/nuclio/nuclio/releases/download/1.13.0/nuctl-1.13.0-darwin-amd64
chmod +x nuctl-1.13.0-darwin-amd64
sudo mv nuctl-1.13.0-darwin-amd64 /usr/local/bin/nuctl
```

Confirm it installed correctly:

```bash
nuctl version
```

---

## Step 4 — Create the AI Project Container

```bash
nuctl create project cvat --platform local
```

---

## Step 5 — Install Segment Anything Model (SAM)

### If your server has an NVIDIA GPU (recommended — much faster for clinicians)

```bash
cd ~/cvat
./serverless/deploy_gpu.sh serverless/pytorch/facebookresearch/sam/
```

### If your server does not have a GPU (works, but slower)

```bash
cd ~/cvat
./serverless/deploy_cpu.sh serverless/pytorch/facebookresearch/sam/
```

This step takes **15–30 minutes** the first time — it downloads and builds the AI model. You will see a lot of log output. This is normal.

When finished, check it is working:

```bash
nuctl get functions --platform local
```

You should see a line with `pth-facebookresearch-sam-vit-h` and STATUS `ready`.

---

## Step 6 — Install the Tracking Model (TransT)

```bash
cd ~/cvat
./serverless/deploy_cpu.sh serverless/pytorch/dschoerk/transt/
```

---

## Step 7 — Confirm the Models Are Working in CVAT

1. Open Google Chrome and go to your CVAT address.
2. Log in.
3. Click **Models** in the top navigation bar.
4. You should see:
   - **Segment Anything** — type: Interactor
   - **TransT** — type: Tracker

If both appear, the setup is complete. Clinicians can now use the AI tools.

---

## Restarting After the Server Reboots

When the server computer is restarted, **the AI models do not restart automatically**. You need to run two commands after every restart:

**1. Start CVAT with AI support:**
```bash
cd ~/cvat
docker compose -f docker-compose.yml \
               -f docker-compose.dev.yml \
               -f components/serverless/docker-compose.serverless.yml \
               up -d
```

**2. Reinstall the AI models:**
```bash
cd ~/cvat
./serverless/deploy_cpu.sh serverless/pytorch/facebookresearch/sam/
./serverless/deploy_cpu.sh serverless/pytorch/dschoerk/transt/
```

> **Tip:** Save these two commands into a text file so you can copy and paste them quickly after each restart.

---

## Troubleshooting AI Models

### "AI tools are missing" — clinician reports no magic wand icon

- Confirm CVAT was started with the AI compose command (Step 2), not the basic `docker compose up -d`.
- Run `nuctl get functions --platform local` — models should show STATUS `ready`.
- If status shows `error`, check the model logs: `docker logs nuclio-nuclio-pth-facebookresearch-sam-vit-h`

### "Port already in use" error when deploying a model

```bash
# Find the old container
docker container ls -a | grep sam
# Remove it (replace CONTAINER_ID with the ID shown)
docker container rm CONTAINER_ID
```

Then redeploy the model.

### SAM is very slow for clinicians

The CPU version runs in 3–10 seconds per click, which is acceptable but not ideal. If your server has an NVIDIA GPU, deploy the GPU version of SAM (use `deploy_gpu.sh` instead of `deploy_cpu.sh` in Step 5).

---

## Next Step

- [Using the AI Tool (SAM)](../clinicians/using-segment-anything-model.md) — share this page with your clinicians
