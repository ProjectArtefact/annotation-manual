# Troubleshooting

This page covers the most common problems encountered when setting up or using CVAT, and how to resolve them.

---

## Installation Issues

### Docker containers fail to start

**Symptom:** Running `docker compose up -d` produces errors, or containers show as `Exited` in `docker compose ps`.

**Solutions:**
1. Check Docker is running: `docker info` (should show server info, not an error).
2. Check for error messages: `docker compose logs`.
3. Ensure you have enough disk space: `df -h` (CVAT needs at least 20 GB free).
4. Try pulling images fresh: `docker compose pull` then `docker compose up -d`.
5. Restart Docker: `sudo systemctl restart docker` (Linux) or restart Docker Desktop (Windows/Mac).

---

### "Port 8080 is already in use"

**Symptom:** CVAT fails to start because port 8080 is occupied by another application.

**Solutions:**
1. Find what is using port 8080: `sudo lsof -i :8080` (Linux/Mac) or `netstat -ano | findstr 8080` (Windows).
2. Stop the conflicting application.
3. Or change CVAT's port by editing `docker-compose.yml` and changing `"8080:80"` to `"8090:80"` (then access CVAT on port 8090).

---

### Cannot connect to CVAT from another machine

**Symptom:** The CVAT server works on `localhost:8080` but other annotators cannot reach it.

**Solutions:**
1. Ensure `CVAT_HOST` was set correctly before starting: `export CVAT_HOST=YOUR-SERVER-IP`, then restart CVAT.
2. Check firewall: allow inbound connections on port 8080.
   - Ubuntu: `sudo ufw allow 8080`
3. Verify other machines can ping the server: `ping YOUR-SERVER-IP`.
4. Confirm the CVAT container is bound to all interfaces: `docker compose ps` should show `0.0.0.0:8080->80/tcp`.

---

### CVAT health check fails — low disk space

**Symptom:** Error: `DiskUsage warning: 94.8% disk usage exceeds 90%`

**Solution:** Free up disk space or increase the health check threshold:

```bash
export CVAT_HEALTH_DISK_USAGE_MAX=95
docker compose down && docker compose up -d
```

---

## Login and Account Issues

### "You do not have permission to perform this action"

**Cause:** The user account exists but has not been added to an organisation or given appropriate permissions.

**Solution:**
1. Log in as the administrator.
2. Go to the organisation → Members → add the user and assign them a role.
3. Or go to the admin panel (`/admin/`) and assign the user to the appropriate Django groups.

---

### Forgot administrator password

**Solution:** Reset it from the command line on the server:

```bash
docker exec -it cvat_server bash -ic 'python3 ~/manage.py changepassword <username>'
```

Replace `<username>` with the admin username.

---

## Annotation Editor Issues

### Canvas is blank / video does not load

**Causes and solutions:**
1. **Wrong browser:** CVAT only works in **Google Chrome**. Switch to Chrome if using any other browser.
2. **Video format not supported:** Convert your video to MP4 (H.264) and re-upload.
3. **Video still processing:** After uploading, CVAT processes the video in the background. Wait a minute and refresh.
4. **Cache issue:** Hard-refresh the page: `Ctrl + Shift + R` (Windows/Linux) or `Cmd + Shift + R` (Mac).

---

### Annotations not saving

**Symptom:** Changes disappear after refreshing.

**Solutions:**
1. Always manually save with `Ctrl + S` — CVAT does not auto-save.
2. Check for a red error notification after saving — this indicates a network or server error.
3. Ensure you are connected to the server (check the browser's network tab or try refreshing the page).

---

### Undo not working as expected

**Note:** In CVAT, `Ctrl + Z` undoes changes within the current editing session but **only up to the last save point**. Once you save, you cannot undo before that save. To recover an earlier version, you would need to re-annotate.

---

### Drawing tools not responding

**Solutions:**
1. Make sure you have clicked on the canvas area (not the sidebar or toolbar).
2. Press `Esc` to deselect any current action, then try again.
3. Check that you are not in a "zoom" mode — some scroll positions lock the canvas. Press `Shift + B` to fit the frame and reset the view.

---

## AI Tools Issues

### AI tools panel shows no models

**Cause:** AI models (Nuclio serverless functions) have not been deployed, or CVAT was not started with serverless support.

**Solutions:**
1. Confirm CVAT was started with: `docker compose -f docker-compose.yml -f docker-compose.dev.yml -f components/serverless/docker-compose.serverless.yml up -d`
2. Check if Nuclio is running: `docker ps | grep nuclio` — should show a running container.
3. Deploy models as described in [Installing AI Models](Installing-AI-Models).
4. Check the models panel: navigate to `http://YOUR-SERVER:8080/models` — deployed models should be listed.

---

### SAM takes very long (30+ seconds per click)

**Cause:** SAM is running on CPU instead of GPU.

**Solutions:**
1. If your server has an NVIDIA GPU, redeploy SAM using the GPU script: `./serverless/deploy_gpu.sh serverless/pytorch/facebookresearch/sam/`
2. Check the GPU is recognised: `nvidia-smi` (should list your GPU and driver version).
3. Ensure NVIDIA Container Toolkit is installed: follow [NVIDIA's guide](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html).

---

### Tracking drifts immediately / produces poor results

**Causes and solutions:**
1. **Object too small:** Zoom in and draw a tighter bounding box — trackers need a minimum object size to lock onto.
2. **Initial box too large:** The tracker includes background in its appearance model. Draw the box as tightly as possible around the object.
3. **Rapid camera or object movement:** Track in shorter segments (5–10 frames at a time) and correct more frequently.
4. **Occlusion:** When an object is occluded, stop the track, mark as "outside", then restart the track when the object reappears.

---

### "Function not ready" error when using AI tools

**Cause:** The AI model container is starting up or crashed.

**Solutions:**
1. Wait 30 seconds and try again (containers take time to initialise after restart).
2. Check function status: `nuctl get functions --platform local` — status should be `ready`, not `error`.
3. If status is `error`, check logs: `docker logs nuclio-nuclio-pth-facebookresearch-sam-vit-h` (replace with your model name).
4. Redeploy the model: `./serverless/deploy_cpu.sh serverless/pytorch/facebookresearch/sam/`

---

## Video / File Issues

### Video upload fails or stalls

**Solutions:**
1. Check the video file size — very large files (>10 GB) may time out. Split the video into smaller segments if needed.
2. Try a different video format. Convert to MP4 (H.264) using FFmpeg.
3. Check server disk space: `df -h`.
4. Check the network connection between your computer and the server.

---

### Video plays incorrectly (wrong frame order, missing frames)

**Cause:** Variable frame rate (VFR) video files can cause frame ordering issues in CVAT.

**Solution:** Convert to constant frame rate (CFR) before uploading:

```bash
ffmpeg -i input.mp4 -vf fps=25 -c:v libx264 -crf 23 output_cfr.mp4
```

Replace `25` with your video's target frame rate.

---

## Getting Additional Help

If your issue is not resolved by this guide:

1. Check the official [CVAT documentation](https://docs.cvat.ai).
2. Search the [CVAT GitHub Issues](https://github.com/cvat-ai/cvat/issues) — your problem may already be reported with a solution.
3. Post in the [CVAT GitHub Discussions](https://github.com/cvat-ai/cvat/discussions) or the CVAT Discord/Slack community.
4. Contact your organisation's server administrator if the issue is infrastructure-related.
