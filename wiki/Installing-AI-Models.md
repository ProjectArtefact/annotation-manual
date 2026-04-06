# Installing AI Models (Nuclio + SAM)

This page is for **server administrators** only. It explains how to deploy the AI models that enable AI-assisted annotation in CVAT — specifically the Segment Anything Model (SAM) and the TransT tracking model.

> Annotators do not need to do anything on this page. Once models are deployed, they will appear automatically in the annotation editor.

---

## Overview

CVAT uses **Nuclio** — a serverless platform — to run AI models as background services. The process is:

1. Rebuild CVAT with serverless (Nuclio) support enabled.
2. Install the `nuctl` command-line tool.
3. Deploy individual AI model functions using `nuctl`.
4. Verify the models appear in CVAT.

---

## Step 1 — Stop the Existing CVAT Containers

If CVAT is already running, stop it first:

```bash
cd ~/cvat
docker compose down
```

---

## Step 2 — Rebuild CVAT with Serverless Support

Restart CVAT with the additional serverless configuration file. This enables the Nuclio platform alongside CVAT.

```bash
cd ~/cvat
docker compose -f docker-compose.yml \
               -f docker-compose.dev.yml \
               -f components/serverless/docker-compose.serverless.yml \
               up -d --build
```

> This command takes longer than the standard startup because it also builds development components. Allow **10–20 minutes** on first run.

Verify that Nuclio is running:

```bash
docker compose -f docker-compose.yml \
               -f docker-compose.dev.yml \
               -f components/serverless/docker-compose.serverless.yml ps
```

You should see a `nuclio` container in the list with status `Up (healthy)`.

---

## Step 3 — Install the `nuctl` Command-Line Tool

`nuctl` is Nuclio's command-line tool for deploying functions. Download the version that matches your operating system.

### Ubuntu / Linux

```bash
# Download nuctl (check https://github.com/nuclio/nuclio/releases for the latest version)
wget https://github.com/nuclio/nuclio/releases/download/1.13.0/nuctl-1.13.0-linux-amd64
chmod +x nuctl-1.13.0-linux-amd64
sudo mv nuctl-1.13.0-linux-amd64 /usr/local/bin/nuctl
```

Verify the installation:

```bash
nuctl version
```

### macOS

```bash
wget https://github.com/nuclio/nuclio/releases/download/1.13.0/nuctl-1.13.0-darwin-amd64
chmod +x nuctl-1.13.0-darwin-amd64
sudo mv nuctl-1.13.0-darwin-amd64 /usr/local/bin/nuctl
```

### Windows (WSL)

Run these commands inside your WSL Linux terminal:

```bash
wget https://github.com/nuclio/nuclio/releases/download/1.13.0/nuctl-1.13.0-linux-amd64
chmod +x nuctl-1.13.0-linux-amd64
sudo mv nuctl-1.13.0-linux-amd64 /usr/local/bin/nuctl
```

---

## Step 4 — Create the CVAT Project in Nuclio

```bash
nuctl create project cvat --platform local
```

Verify there are no existing functions yet:

```bash
nuctl get functions --platform local
```

It should return: `No functions found`

---

## Step 5 — Deploy Segment Anything Model (SAM)

SAM allows annotators to click on an object and get an instant precise segmentation. It is the most important AI tool for clinical annotation.

### CPU version (works on any server, slower)

```bash
cd ~/cvat
./serverless/deploy_cpu.sh serverless/pytorch/facebookresearch/sam/
```

This will take **15–30 minutes** the first time as it builds a Docker image for the model.

### GPU version (requires NVIDIA GPU, much faster — recommended)

```bash
cd ~/cvat
./serverless/deploy_gpu.sh serverless/pytorch/facebookresearch/sam/
```

> **GPU deployment note:** Only run one GPU-based serverless function at a time, as GPU memory is shared. If you plan to run both SAM and a tracking model simultaneously, a GPU with 16 GB+ VRAM is recommended.

### Verifying SAM is deployed

```bash
nuctl get functions --platform local
```

You should see `pth-facebookresearch-sam-vit-h` in the list with STATE `ready`.

---

## Step 6 — Deploy the Tracking Model (TransT)

TransT is a transformer-based tracker that follows objects across video frames automatically.

```bash
cd ~/cvat
nuctl create project cvat --platform local
nuctl deploy --project-name cvat \
             --path serverless/pytorch/dschoerk/transt/nuclio \
             --platform local
```

Or use the CPU deploy script:

```bash
./serverless/deploy_cpu.sh serverless/pytorch/dschoerk/transt/
```

---

## Step 7 — Verify Models in CVAT

1. Open Google Chrome and go to your CVAT address.
2. Log in.
3. Click **Models** in the top navigation bar.
4. You should see:
   - **Segment Anything Model (SAM)** — type: Interactor
   - **TransT** — type: Tracker

If you see these models listed, the deployment was successful.

You can also verify by opening any task's annotation editor and clicking the **magic wand** icon in the left panel — the models should appear in the AI tools panel.

---

## Keeping AI Models Running After a Restart

When you restart the CVAT Docker containers, the AI model containers are **not** automatically restarted. You will need to redeploy them each time CVAT is restarted.

To make this easier, you can create a small shell script:

```bash
# Save as ~/cvat/deploy_ai_models.sh
#!/bin/bash
cd ~/cvat
./serverless/deploy_cpu.sh serverless/pytorch/facebookresearch/sam/
./serverless/deploy_cpu.sh serverless/pytorch/dschoerk/transt/
```

```bash
chmod +x ~/cvat/deploy_ai_models.sh
```

Run `~/cvat/deploy_ai_models.sh` after each CVAT restart to restore AI functionality.

---

## Restarting CVAT with Serverless Support

Whenever you restart CVAT, use the extended command (not the basic `docker compose up -d`):

```bash
cd ~/cvat
docker compose -f docker-compose.yml \
               -f docker-compose.dev.yml \
               -f components/serverless/docker-compose.serverless.yml \
               up -d
```

Then run your AI models deployment script.

---

## Troubleshooting

### Models show as "error" in `nuctl get functions`

```bash
# Check the logs for the failing model container
docker logs nuclio-nuclio-pth-facebookresearch-sam-vit-h
```

### Port already allocated error

If you see a port conflict error when deploying a model:

```bash
# Find and remove the old container
docker container ls -a | grep sam
docker container rm <CONTAINER_ID>
```

Then redeploy the model.

### Models not appearing in CVAT interface

- Ensure CVAT was started with the serverless compose file (Step 2).
- Check the CVAT server logs: `docker logs cvat_server`
- Check Nuclio dashboard at `http://localhost:8070` — models should appear there.

### Out of memory when deploying GPU model

- Reduce the number of GPU functions deployed simultaneously.
- Use the CPU version of the models if GPU memory is insufficient.

---

## Next Step

- [Using Segment Anything Model (SAM)](Using-Segment-Anything-Model)
- [Video Object Tracking](Video-Object-Tracking)
