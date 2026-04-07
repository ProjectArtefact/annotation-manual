# Clinician Guide: Connecting, Annotating, and Reviewing

This is the main guide for clinicians. It covers everything from connecting to CVAT for the first time, through annotating your assigned videos, to reviewing a colleague's work.

**Jump to the section you need:**

- [Every-session quick start](#every-session-quick-start)
- [Connecting for the first time — Mac](#connecting-for-the-first-time-mac)
- [Connecting for the first time — Windows](#connecting-for-the-first-time-windows)
- [Logging In to CVAT](#logging-in-to-cvat)
- [Finding Your Assigned Task](#finding-your-assigned-task)
- [Finishing Your Annotation Task](#finishing-your-annotation-task)
- [Reviewing Another Clinician's Work](#reviewing-another-clinicians-work)
- [Common Questions](#common-questions)

---

## What Is the SSH Tunnel?

CVAT runs on a university PC. To access it securely from your own laptop, you create an **SSH tunnel** — think of it as a private, encrypted phone call between your laptop and the university PC. While the call is connected, CVAT appears at a normal web address in Chrome. When you hang up (close the terminal), CVAT stops being accessible.

You need to do this **every time** you want to use CVAT.

---

## Every-Session Quick Start

Once you have connected for the first time (see below), here is all you need to do each session:

> **What the coordinator will give you (save these somewhere):**
> - **IP address** of the university PC — e.g. `130.251.10.25`
> - **SSH username** — e.g. `clinician1`
> - **SSH password**
> - **CVAT username** and **CVAT password** *(these are different from your SSH password)*

| Step | Mac | Windows |
|------|-----|---------|
| 1. Open a terminal | Press `Cmd+Space`, type `Terminal`, press Enter | Press `Win` key, type `cmd`, press Enter |
| 2. Run the SSH command | `ssh -L 8080:localhost:8080 YOUR-USERNAME@IP-ADDRESS` | `ssh -L 8080:localhost:8080 YOUR-USERNAME@IP-ADDRESS` |
| 3. Enter your SSH password | Type it (nothing appears — this is normal) | Type it (nothing appears — this is normal) |
| 4. Keep the terminal open | Do not close this window | Do not close this window |
| 5. Open Chrome | Go to `http://localhost:8080` | Go to `http://localhost:8080` |
| 6. Log in | Use your **CVAT** username and password | Use your **CVAT** username and password |

---

## Connecting for the First Time — Mac

### Step 1 — Open the Terminal app

The Terminal is a built-in app on every Mac. You do not need to install anything.

1. Press **`Command (⌘) + Space`** together to open Spotlight Search.
2. Type **`Terminal`**.
3. Press **Enter**.

A white or black window opens with a blinking cursor. This is the Terminal. It looks plain and technical but you only need to type one command.

---

### Step 2 — Type the SSH command

Click inside the terminal window so it is active. Carefully type the command below — **replace** `YOUR-USERNAME` and `IP-ADDRESS` with the details the coordinator gave you:

```
ssh -L 8080:localhost:8080 YOUR-USERNAME@IP-ADDRESS
```

**Filled-in example** (your values will be different):
```
ssh -L 8080:localhost:8080 clinician1@130.251.10.25
```

Press **Enter**.

> **Common mistake:** Make sure there are no extra spaces and no line breaks. The whole command goes on one line.

---

### Step 3 — First-time security question

The very first time you connect, you will see a message like this:

```
The authenticity of host '130.251.10.25' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Type **`yes`** and press Enter. You will only see this once — it will not ask again on future connections.

---

### Step 4 — Enter your SSH password

You will see:

```
clinician1@130.251.10.25's password:
```

Type your **SSH password** (the one the coordinator gave you) and press Enter.

> **Important:** As you type the password, nothing appears on screen — no dots, no asterisks. This is normal and intentional. Just type it carefully and press Enter.

---

### Step 5 — You are connected

If the password is correct, you will see something like:

```
Welcome to Ubuntu 22.04 LTS
clinician1@cvat-server:~$
```

The `$` at the end means the connection is active and working.

> **Do not close this Terminal window** while you are using CVAT. Keep it open in the background — you can minimise it. If you accidentally close it, just repeat Steps 1–5.

---

### Step 6 — Open CVAT in Chrome

Open **Google Chrome** (not Safari, not Firefox). Type this address in the address bar:

```
http://localhost:8080
```

Press Enter. The CVAT login page should appear. If it does not, check that the Terminal window is still open and the SSH command completed successfully.

---

### When You Are Done

When you have finished annotating for the session:
1. Save your work in CVAT: **`Cmd + S`**
2. Close the Chrome tab.
3. Go back to the Terminal window and type `exit`, then press Enter — or simply close the Terminal window.

---

## Connecting for the First Time — Windows

Most Windows computers (Windows 10 and Windows 11) have SSH built in. You access it through the **Command Prompt** — a window where you type simple commands.

> **If the SSH command does not work** (you get an error saying it is not recognised), skip to [Using PuTTY instead](#alternative-using-putty-on-windows) at the bottom of this section.

---

### Step 1 — Open Command Prompt

**Option A — Start menu:**
1. Click the **Start button** (Windows logo, bottom-left).
2. Type **`cmd`**.
3. Click **Command Prompt** in the results.

**Option B — Keyboard shortcut:**
1. Press **`Windows key + R`** together.
2. Type **`cmd`** and press Enter.

A black window with white text opens, ending with something like `C:\Users\YourName>`. This is the Command Prompt.

---

### Step 2 — Type the SSH command

Click inside the Command Prompt window. Type the command below — **replace** `YOUR-USERNAME` and `IP-ADDRESS` with what the coordinator gave you:

```
ssh -L 8080:localhost:8080 YOUR-USERNAME@IP-ADDRESS
```

**Filled-in example** (your values will be different):
```
ssh -L 8080:localhost:8080 clinician1@130.251.10.25
```

Press **Enter**.

> **Tip:** You can right-click inside the Command Prompt window to paste if you have copied the command.

---

### Step 3 — First-time security question

The very first time you connect, you will see:

```
The authenticity of host '130.251.10.25' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

Type **`yes`** and press Enter. This only appears once.

---

### Step 4 — Enter your SSH password

You will see:

```
clinician1@130.251.10.25's password:
```

Type your **SSH password** and press Enter.

> **Important:** Nothing appears as you type — no dots, no asterisks. This is completely normal. Type your password carefully and press Enter.

---

### Step 5 — You are connected

If successful, you will see something like:

```
Welcome to Ubuntu 22.04 LTS
clinician1@cvat-server:~$
```

The `$` sign means you are connected.

> **Do not close this Command Prompt window** while using CVAT. Minimise it and leave it running in the background.

---

### Step 6 — Open CVAT in Chrome

Open **Google Chrome**. In the address bar at the top, type:

```
http://localhost:8080
```

Press Enter. The CVAT login page should appear.

---

### When You Are Done

1. Save your work in CVAT: **`Ctrl + S`**
2. Close the Chrome tab.
3. In the Command Prompt window, type `exit` and press Enter — or close the window.

---

### Alternative: Using PuTTY on Windows

If the SSH command in Command Prompt does not work, PuTTY is a free, easy-to-use alternative with a graphical interface.

**Step 1 — Download PuTTY**

Go to [putty.org](https://www.putty.org/) and click **Download PuTTY**. Run the installer.

**Step 2 — Set up the SSH tunnel**

1. Open PuTTY from the Start menu.
2. In the **Host Name** box, type: `YOUR-USERNAME@IP-ADDRESS`
   - Example: `clinician1@130.251.10.25`
3. Make sure **Port** is `22` and **SSH** is selected.
4. In the **left panel**, click **Connection → SSH → Tunnels**.
5. Fill in:
   - **Source port:** `8080`
   - **Destination:** `localhost:8080`
6. Click the **Add** button. You should see `L8080  localhost:8080` appear in the list above.
7. Go back to **Session** in the left panel.
8. In the **Saved Sessions** box, type a name (e.g. `CVAT`) and click **Save** — so you don't have to set this up again next time.
9. Click **Open**.

**Step 3 — Log in**

A black terminal window opens and asks for your password. Type your **SSH password** and press Enter. (Nothing appears as you type — this is normal.)

You will see a `$` prompt when connected. Keep this window open.

**Step 4 — Open Chrome**

Go to `http://localhost:8080` in Google Chrome.

**Next time:** Open PuTTY, double-click `CVAT` in the Saved Sessions list, enter your password, and open Chrome. That's it.

---

## Logging In to CVAT

Once Chrome shows `http://localhost:8080`, you will see the CVAT login page.

1. Enter your **CVAT username** and **CVAT password**.
   - These are **different** from your SSH password — the coordinator gives you both sets separately.
2. Click **Login**.

You should now see the CVAT dashboard showing your projects and tasks.

---

## Finding Your Assigned Task

1. Click **Tasks** in the navigation bar at the top of the page.
2. Look for your name in the **Assignee** column. Click the task name.
3. Click the **Job** link that appears. The annotation editor opens with your video.

**If no tasks appear:**

You may need to switch into the study group first:
1. Click your name or avatar in the **top-right corner**.
2. Look for an **Organization** entry in the dropdown menu.
3. Click the study name (e.g. `polyp-study-2026`).
4. The page refreshes and your tasks should now appear.

If tasks are still missing, email [ameya.pore@univr.it](mailto:ameya.pore@univr.it).

---

## Annotating Your Task

For the full annotation guide, see:
- [Video Annotation Basics](video-annotation-basics.md) — the step-by-step workflow
- [Annotation Types](annotation-types.md) — what shapes to draw (masks for this study)
- [Using the AI Tool (SAM)](using-segment-anything-model.md) — click-to-segment with AI
- [Video Object Tracking](video-object-tracking.md) — AI tracking across frames

---

## Finishing Your Annotation Task

When you have finished annotating all frames in your task:

**1. Check your work** using this list:
- [ ] Every lesion annotated on every frame it is visible
- [ ] Masks cover the structure accurately — zoom in (`+` key) to check edges
- [ ] Correct label used (e.g. "polyp")
- [ ] Object marked as "Outside" when it leaves the frame

**2. Save:** Press `Ctrl + S` (Windows) or `Cmd + S` (Mac).

**3. Mark as finished:**
- Click the **Menu button (≡)** in the top-right corner of the annotation editor.
- Select **Finish the job**.

**4. Notify the coordinator:** Email [ameya.pore@univr.it](mailto:ameya.pore@univr.it) to say you have finished, and mention if you are ready to review a colleague's task.

---

## Reviewing Another Clinician's Work

The coordinator will tell you which colleague's task to review. Here is the full process.

> **Note:** To approve or reject a task, your CVAT account must have the **Supervisor** role. The coordinator sets this up. If you see a "permission denied" message, email [ameya.pore@univr.it](mailto:ameya.pore@univr.it).

---

### Step 1 — Connect and log in

Follow the connection steps above (same as for annotating). Log in to CVAT.

---

### Step 2 — Find the task to review

1. Click **Tasks** in the top navigation bar.
2. Find the task that has your **colleague's name** as Assignee (not your name).
3. Click the task name to open it.

---

### Step 3 — Signal that you are reviewing it

1. In the job row, find the **Stage** dropdown.
2. Change it from **Annotation** to **Validation**.
3. Click **Save**.

This shows the coordinator and your colleague that you are actively reviewing the task.

---

### Step 4 — Open and review the annotations

Click the **Job** link to open the annotation editor.

Step through every frame using:
- **`F`** → next frame
- **`D`** → previous frame

For each frame, check:

| What to check | What to look for |
|---------------|-----------------|
| **Coverage** | Every frame where the lesion is visible should have a mask |
| **Accuracy** | The mask should cover the full lesion — press `+` to zoom in and inspect the edges |
| **Label** | The correct label name should be shown (e.g. "polyp") |
| **Outside marking** | When the lesion disappears from view, the annotation should be marked Outside — not left sitting on a blank area |
| **No phantom annotations** | There should be no masks on frames where the lesion is not present |

---

### Step 5 — Accept or send back

**If the work is correct:**

1. Go back to **Tasks** (click Tasks in the top bar).
2. Open the task and find the job.
3. Change **Stage** to **Acceptance**.
4. Click **Save**.
5. Email your colleague and the coordinator to confirm.

**If corrections are needed:**

1. Make a note of the **frame numbers** and what is wrong.
2. Change the **Stage** back to **Annotation**.
3. Click **Save**.
4. Email your colleague with specific feedback, for example:
   > *"Frame 47 — the mask does not cover the lower edge of the polyp. Frame 83 — annotation is missing entirely."*

---

### Responding to Review Feedback (When Your Work Is Sent Back)

1. Connect via SSH and log in as normal.
2. Open your task — it will now show as **Annotation** stage again.
3. Go to the specific frame numbers mentioned in the feedback.
4. Fix the annotations.
5. Save: `Ctrl + S` (Windows) or `Cmd + S` (Mac).
6. Click **Menu (≡) → Finish the job**.
7. Email the reviewer to say corrections are done.

---

## What Happens to the Annotations?

- All annotations are stored on the university PC. You do not need to send files to anyone.
- If you and your colleague annotated **different videos**, the coordinator gets one combined file when they export — nothing to merge.
- If you both annotated the **same video** (consistency check), the coordinator exports them separately and compares them.

---

## Common Questions

**Do I need to keep the terminal/Command Prompt window open the whole time?**
Yes. The terminal window is what keeps the secure connection alive. If you close it, `http://localhost:8080` will stop loading. Just re-run the SSH command and refresh Chrome to reconnect.

**I typed my password but it says "Permission denied"**
Check that you typed the correct SSH username and password (not your CVAT password). If you are unsure, ask the coordinator to reset your SSH password.

**The terminal connected but Chrome shows "This site can't be reached"**
The SSH tunnel connects to port 8080. Make sure the address in Chrome is exactly `http://localhost:8080` — not `https://` and not just `localhost`.

**Nothing happens after I type the SSH command**
Wait up to 10 seconds. If still nothing, check your network connection and confirm the IP address with the coordinator.

**What if the connection drops while I am annotating?**
Your last saved annotations are safe on the university PC. Re-run the SSH command, open Chrome at `http://localhost:8080`, log back in, and reopen your task. Only changes since your last `Ctrl + S` / `Cmd + S` will be lost.

**Can both clinicians use CVAT at the same time?**
Yes. Multiple people can be connected and annotating simultaneously without any problems.
