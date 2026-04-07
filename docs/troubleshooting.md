# Troubleshooting

Solutions to the most common problems. If your issue is not listed here, contact [ameya.pore@univr.it](mailto:ameya.pore@univr.it).

---

## Problems Clinicians May Have

### "The SSH command gives an error / 'ssh is not recognized'"

**On Windows:** Command Prompt and PowerShell have SSH built in on Windows 10 and 11. If you get "ssh is not recognized", your Windows version may be older. Use PuTTY instead — see [Using PuTTY on Windows](clinicians/clinician-workflow.md#alternative-using-putty-on-windows).

**Connection refused error:** The server may be offline or the IP address may have changed. Email [ameya.pore@univr.it](mailto:ameya.pore@univr.it).

**Permission denied (wrong password):** Make sure you are typing the **SSH** password, not the CVAT password — these are two different passwords. Ask the coordinator to confirm or reset your SSH password.

---

### "localhost:8080 says 'This site can't be reached' in Chrome"

The SSH tunnel is not active. Check:
1. Your terminal or Command Prompt window is still open — it **must** stay open while you use CVAT.
2. The SSH command finished and shows a `$` prompt. If it timed out or you closed the window, re-run the SSH command and refresh Chrome.
3. Make sure you typed `http://localhost:8080` — not `https://` and not just `localhost`.

---

### "I see a message about 'authenticity of host' when connecting"

This is a normal first-time security check. Type `yes` and press Enter. You will only see it once.

---

### "I can't see any tasks in my task list"

**Cause 1 — You are not in the right study group.**
1. Click your name/avatar in the **top-right corner**.
2. Look for an **Organization** section in the dropdown.
3. Click the study name to switch into it.
4. Your tasks should now appear.

**Cause 2 — No tasks have been assigned to you yet.**
Contact your study coordinator.

---

### "The CVAT page won't open in my browser"

- Make sure you are using **Google Chrome** — CVAT does not work in Firefox, Safari, or Edge.
- Check that you typed the address correctly (e.g. `http://192.168.1.50:8080`).
- Check that the server computer is switched on and connected to the network.
- If using a laptop connected to a different Wi-Fi network than the server, you may not be able to connect. Ask your study coordinator.

---

### "The video frame is blank / the video won't load"

1. Try a hard refresh: press `Ctrl + Shift + R` (Windows) or `Cmd + Shift + R` (Mac).
2. If still blank, the video file may be in a format CVAT cannot display. Let your study coordinator know.

---

### "My annotations disappeared"

CVAT does **not** auto-save. If you navigated away or the session timed out before saving, your most recent changes may be lost.

- Always save with **`Ctrl + S`** every 5–10 frames.
- Annotations you saved before the session ended are still there — only changes made since the last save are lost.

---

### "The AI tool (magic wand) is missing or has no options"

The AI tools have not been set up on the server yet. Contact your study coordinator to set them up (see [Installing AI Models](coordinator/installing-ai-models.md)).

---

### "SAM is taking a very long time (more than 10 seconds per click)"

This is expected on a server without a GPU. The AI still works — it is just slower. If speed is a problem, let your study coordinator know so they can look into a GPU upgrade.

---

### "I accidentally deleted an annotation — can I get it back?"

Press **`Ctrl + Z`** immediately to undo. This works as long as you have not saved yet.

If you have already saved after the deletion, the annotation cannot be recovered. You will need to draw it again.

---

### "I cannot change the task stage (getting a permission error when reviewing)"

Your CVAT account has the **Worker** role instead of **Supervisor**. Workers can only annotate their own tasks — they cannot change task stages.

Contact [ameya.pore@univr.it](mailto:ameya.pore@univr.it) and ask to have your role changed to **Supervisor** in the organisation.

---

### "The brush tool is not painting where I click"

- Make sure you clicked on the **canvas** (the video image itself), not on the toolbar or panel.
- Press `Esc` first to cancel any active mode, then press `B` to reactivate the brush.
- Try zooming in: press `+` or scroll up with the mouse wheel.

---

## Problems the Person Who Set Up CVAT May Have

### CVAT won't start after installation

1. Check Docker is running: open Docker Desktop (Windows/Mac) or run `docker info` in a terminal.
2. Check for error messages: `docker compose logs`
3. Check free disk space — CVAT needs at least 20 GB free: `df -h` (Linux/Mac)
4. Restart Docker and try again: `docker compose down` then `docker compose up -d`

---

### "Port 8080 is already in use" error

Another application on the server is using port 8080.

**Find and stop the conflicting app:**
- Linux/Mac: `sudo lsof -i :8080`
- Windows: `netstat -ano | findstr 8080`

Or change CVAT to use a different port by editing `docker-compose.yml` and changing `"8080:80"` to `"8090:80"` — then access CVAT at port 8090.

---

### Clinicians cannot connect from other computers

1. Make sure you set `CVAT_HOST` to the server's IP address **before** starting CVAT (see the [Installation](coordinator/installation.md) guide).
2. On Linux: allow the port through the firewall: `sudo ufw allow 8080`
3. Confirm the server's IP address has not changed (e.g. after a restart). If it has, stop CVAT, update the IP address, and restart.

---

### Someone cannot see their tasks / has no access

1. Make sure they have been added to the organisation: go to the organisation settings → **Members** tab → add them.
2. Make sure their task is assigned to them: open the task → expand the job → set the **Assignee** field to their username.

---

### Forgot the main account password

Run this command on the server (replace `yourusername` with the actual username):

```bash
docker exec -it cvat_server bash -ic 'python3 ~/manage.py changepassword yourusername'
```

---

### AI models disappeared after the server restarted

This is expected — AI models do not restart automatically. After every server restart:

1. Start CVAT with the AI compose command (see [Installing AI Models](coordinator/installing-ai-models.md#restarting-after-the-server-reboots)).
2. Redeploy the models using the deploy scripts.

---

### CVAT health check warning about disk space

```
DiskUsage warning: 94% disk usage exceeds 90%
```

Free up disk space on the server, or run:

```bash
export CVAT_HEALTH_DISK_USAGE_MAX=95
docker compose down && docker compose up -d
```

---

## Still stuck?

Contact [ameya.pore@univr.it](mailto:ameya.pore@univr.it) or check the official CVAT documentation at [docs.cvat.ai](https://docs.cvat.ai).
