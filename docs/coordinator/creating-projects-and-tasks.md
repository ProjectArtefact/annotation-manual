# Creating Projects and Tasks

> **This page is for the study coordinator (Amey).** Clinicians do not need to create projects or tasks — they only need to open their assigned task and annotate. Go to [Clinician Workflow](../clinicians/clinician-workflow.md) instead.

---

## What Is a Project and What Is a Task?

Think of it this way:

- A **Project** is the whole study (e.g. "Colonoscopy Polyp Study 2026"). It holds all the settings and label definitions.
- A **Task** is one video from that study (e.g. "Patient_001"). Each video gets its own task.
- A **Job** is a portion of a task. If a video is very long, you can split it into segments and assign each segment to a different clinician.

Labels you define on the project are shared across all its tasks — you only need to set them up once.

---

## Step 1 — Create a Project

1. From the main dashboard, click **Projects** in the top navigation bar.
2. Click **+ Create a new project**.
3. Give the project a **Name** (e.g. `Colonoscopy Polyp Study 2026`).
4. Define your **labels** (see below).
5. Click **Submit**.

### Defining Labels

Labels are the categories your clinicians will annotate (e.g. "polyp", "lesion", "instrument").

For each label:

1. Click **Add label**.
2. Type the label **name** (e.g. `polyp`).
3. Choose a **colour** — pick a different colour for each label so they are easy to tell apart on screen.
4. Click the **tick** to confirm.
5. Repeat for all labels.

### Adding Extra Information to Labels (Attributes)

If you need clinicians to record extra details about each annotation (e.g. polyp type, size category), you can add attributes:

1. On the label, click **Add attribute**.
2. Give it a name (e.g. `morphology`).
3. Choose the type of input:
   - **Select** — a dropdown list (e.g. pedunculated / sessile / flat)
   - **Checkbox** — a yes/no tick
   - **Text** — free text
   - **Number** — a number with a range
4. For a **Select** type, type each option and press Enter after each one.
5. Tick **Required** if clinicians must fill this in.

---

## Step 2 — Create a Task (one per video)

1. Open your project and click **+ Create new task** inside it.
2. Fill in the **Name** — use something clear, e.g. `Patient_001_20260401`.
3. The project's labels are inherited automatically — you do not need to re-enter them.
4. Under **Files**, upload the video (see [Uploading Videos](uploading-videos.md)).
5. Leave all other settings at their defaults unless you have a specific reason to change them.
6. Click **Submit & Open**.

### Settings You May Want to Change

You only need to touch these if you have a specific need:

| Setting | What it does | Default |
|---------|-------------|---------|
| **Frame step** | Annotate every Nth frame (e.g. 5 = every 5th frame) | 1 = every frame |
| **Segment size** | Split the video into sections for multiple annotators | 0 = one section |
| **Start / Stop frame** | Annotate only part of the video | Full video |

---

## Step 3 — Assign the Task to a Clinician

After creating the task, CVAT creates one or more **Jobs** inside it. Assign each job to the relevant clinician:

> **Reminder:** Clinicians must have the **Supervisor** role in the organisation (set during [First Login and Setup](first-login-and-setup.md#step-5-invite-clinicians-to-the-organisation-and-set-them-as-supervisors)) to be able to review and approve each other's work. Workers can only annotate — they cannot change task stages.

1. Open the task by clicking its name.
2. You will see a list of **Jobs**.
3. Click on a job to expand it.
4. In the **Assignee** field, search for and select the clinician's username.
5. Click **Save**.

The clinician will now see this job in their task list when they log in.

---

## Step 4 — Track Progress

Jobs move through three stages:

| Stage | Meaning |
|-------|---------|
| **Annotation** | The clinician is actively working on it |
| **Validation** | The clinician has finished — you are reviewing it |
| **Acceptance** | Reviewed and approved — ready to export |

To change a job's stage: open the task, expand the job, and change the **Stage** dropdown. Click **Save**.

- When a clinician finishes, change the stage to **Validation** and review the annotations.
- If corrections are needed, change it back to **Annotation** and message the clinician.
- When satisfied, set it to **Acceptance**.

---

## Creating More Tasks (Same Settings)

To add more videos to the same project without re-entering all the settings:

1. On the Tasks page, find an existing task.
2. Click the **⋮ (three-dot menu)** next to it.
3. Select **Copy**.
4. Change the task name and upload the new video file.
5. Click **Submit**.

---

## Next Step

- [Uploading Videos](uploading-videos.md)
