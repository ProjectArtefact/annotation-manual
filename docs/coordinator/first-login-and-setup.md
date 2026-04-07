# First Login and Setup

> **This page is for the study coordinator (Amey).** It covers the one-time setup after CVAT is installed: creating SSH accounts for clinicians on the university PC, creating their CVAT accounts, and organising the project.
>
> **Clinicians:** You do not need to read this. Go to [Clinician Workflow](../clinicians/clinician-workflow.md) for your connection guide.

---

## Overview of What You Need to Set Up

| What | Why |
|------|-----|
| **SSH account** on the university PC | Allows each clinician to securely connect from their own laptop |
| **CVAT account** | Allows each clinician to log in to the annotation tool |
| **Organisation** in CVAT | Groups your project, tasks, and team together |
| **Supervisor role** in CVAT | Allows clinicians to both annotate AND review each other's work |

---

## Step 1 — Log In to CVAT as the Main Admin

1. On the university PC (or via your own SSH tunnel), open **Google Chrome**.
2. Go to `http://localhost:8080`.
3. Log in with the username and password you created during installation.

---

## Step 2 — Create SSH Accounts for Each Clinician

Each clinician needs an account on the university PC (Linux) to be able to connect via SSH.

Open a terminal on the university PC and run (replace `clinician1` with the actual username):

```bash
sudo adduser clinician1
```

You will be prompted to set a password for that user. Write it down — you will share it with the clinician.

Repeat for each clinician:

```bash
sudo adduser clinician2
sudo adduser clinician3
```

> **What to send each clinician:**
> - The IP address of the university PC (e.g. `130.251.10.25`)
> - Their SSH username (e.g. `clinician1`)
> - Their SSH password
> - Their CVAT username and password (created in Step 4 below)
> - A link to the [Clinician Workflow](../clinicians/clinician-workflow.md) page in this wiki

---

## Step 3 — Create an Organisation in CVAT

An Organisation groups your project and team together.

1. Click your name/avatar in the **top-right corner** of CVAT.
2. Select **Create organization**.
3. Fill in:
   - **Short name** — no spaces (e.g. `polyp-study-2026`)
   - **Full name** — readable (e.g. `Endoscopy Polyp Study 2026`)
4. Click **Submit**.

---

## Step 4 — Create CVAT Accounts for Each Clinician

You have two options:

**Option A — You create the account (recommended for full control)**

1. Go to `http://localhost:8080/admin/` in Chrome.
2. Log in with your main account credentials.
3. Click **Users → Add user**.
4. Set a **username** and **password** for the clinician.
5. Click **Save and continue editing**.
6. Scroll down and ensure **Staff status** is NOT ticked (regular user).
7. Click **Save**.
8. Repeat for each clinician.

**Option B — Clinician self-registers**

1. Share the CVAT address with the clinician: when they open Chrome at `http://localhost:8080` they can click **Create an account**.
2. Once they register, invite them to the organisation (Step 5 below) before they can see anything.

---

## Step 5 — Invite Clinicians to the Organisation and Set Them as Supervisors

> **Critical:** Clinicians must be set as **Supervisors** (not Workers) so they can both annotate their own tasks AND review and approve/reject other clinicians' tasks. Workers can only annotate their own assigned jobs.

1. In CVAT, click your name in the top-right and switch to your organisation.
2. Click the organisation name to open its settings.
3. Go to the **Members** tab.
4. Click **Invite members**.
5. Enter the clinician's CVAT username.
6. Set their role to **Supervisor**.
7. Click **Add**.

Repeat for each clinician.

---

## Step 6 — Verify a Clinician Can Connect

Ask one clinician to follow the [Clinician Workflow](../clinicians/clinician-workflow.md) connection guide and confirm they can:
1. Connect via SSH tunnel.
2. Open `http://localhost:8080` in Chrome.
3. Log in with their CVAT credentials.
4. See the organisation name in their top-right menu.

If they cannot log in or cannot see the organisation, check:
- Their CVAT account exists and is correctly added to the organisation.
- Their SSH credentials work (try connecting yourself with their username).

---

## Step 7 — Create Tasks and Assign Them

See [Creating Projects and Tasks](creating-projects-and-tasks.md) for the full guide.

Key point: after creating each task, assign it to the relevant clinician in the **Assignee** field of the job. The clinician will not see the task until it is assigned to them.

---

## Changing a Clinician's Password

**SSH password** (Linux account):
```bash
sudo passwd clinician1
```

**CVAT password:**
1. Go to `http://localhost:8080/admin/`
2. Click **Users**, find the clinician.
3. Click **Change password** and set a new one.

---

## Next Step

- [Creating Projects and Tasks](creating-projects-and-tasks.md)
