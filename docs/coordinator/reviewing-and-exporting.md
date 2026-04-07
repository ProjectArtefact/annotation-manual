# Reviewing and Exporting Annotations

This page covers three activities. Jump to the one you need:

- [**Clinician: Finishing your annotation task**](#finishing-your-annotation-task-clinicians)
- [**Clinician: Reviewing a colleague's work**](#reviewing-a-colleagues-work-clinicians) — the peer-review process
- [**Coordinator: Monitoring progress and exporting data**](#monitoring-progress-and-exporting-coordinator)

---

## Finishing Your Annotation Task (Clinicians)

When you have annotated all the frames in your task, do the following before marking it as done.

### Checklist

- [ ] Every lesion or structure is annotated on every frame it is visible
- [ ] Masks cover the structure accurately — zoom in (`+` key) to check the edges
- [ ] Correct label used for each annotation (e.g. "polyp")
- [ ] Object marked as **Outside** on frames where it disappears from the video
- [ ] Work saved (`Ctrl + S`)

### How to submit

1. Press `Ctrl + S` to save.
2. Click the **Menu (≡)** button in the top-right of the annotation editor.
3. Select **Finish the job**.
4. Email [ameya.pore@univr.it](mailto:ameya.pore@univr.it) to notify the coordinator — and let them know if you are available to review a colleague's task.

---

## Reviewing a Colleague's Work (Clinicians)

The coordinator will let you know which task to review and whose work it is.

> **Your account must have Supervisor role** to change task stages (approve or reject). The coordinator sets this when creating your account. If you get "permission denied" when changing a stage, contact [ameya.pore@univr.it](mailto:ameya.pore@univr.it).

For the complete step-by-step review guide including what to check and how to send feedback, see the dedicated section:

**→ [Reviewing Another Clinician's Work](../clinicians/clinician-workflow.md#reviewing-another-clinicians-work)**

### The review stages at a glance

| Stage | Set by | Meaning |
|-------|--------|---------|
| **Annotation** | Coordinator (when task is created) | Clinician is annotating |
| **Validation** | Reviewer clinician | Reviewer has opened the task and is checking it |
| **Acceptance** | Reviewer clinician | Work is approved — ready to export |
| **Annotation** (again) | Reviewer clinician | Work sent back for corrections |

To change the stage: go to **Tasks** → open the task → expand the job → change the **Stage** dropdown → click **Save**.

---

## Monitoring Progress and Exporting (Coordinator)

### Tracking the status of all tasks

Go to **Tasks** in the top navigation bar. You can see all tasks and their current stage at a glance:
- **Annotation** — being worked on
- **Validation** — under peer review
- **Acceptance** — approved, ready to export

---

### Exporting Annotations

Export in **COCO 1.0** format — the standard for training segmentation models.

**Steps:**

1. Go to the **Tasks** page.
2. Click the **⋮ (three-dot menu)** on the right side of the task row.
3. Select **Export task dataset**.
4. Set:
   - **Format:** COCO 1.0
   - **Save images:** ✓ Tick this (includes the video frames as image files — needed for model training)
5. Click **OK**.
6. When ready, the file downloads as a `.zip` to your Downloads folder.

**What the zip contains:**

```
export.zip
├── annotations/
│   └── instances_default.json    ← all mask annotations in COCO format
└── images/
    └── default/
        ├── frame_000001.jpg
        ├── frame_000002.jpg      ← one image per annotated frame
        └── ...
```

**Exporting all clinicians' work together:**
If each clinician annotated different videos (the normal setup), export at the **Project level** to get everything in one file:
1. Go to **Projects** in the top bar.
2. Click the **⋮** menu on the project row.
3. Select **Export project dataset** → COCO 1.0 → tick Save images → OK.

**If two clinicians annotated the same video (inter-rater reliability):**
Export each task separately — one zip per clinician. Send both to your ML engineer for comparison (Dice coefficient, IoU etc.).

---

### Backing Up the Data

**Back up regularly.** The university PC is the only place where annotations are stored.

#### Weekly: Export all completed tasks

1. For each task that has reached **Acceptance** stage, export it as COCO 1.0.
2. Save the zip files to a location separate from the university PC — for example:
   - University shared drive (e.g. your institution's network storage)
   - University-managed cloud storage (OneDrive for Business, SharePoint)

#### Weekly: Full server backup (captures everything — accounts, tasks, all annotations)

Run this on the university PC:

```bash
cd ~/cvat
docker exec cvat_db pg_dump -U root cvat > cvat_backup_$(date +%Y%m%d).sql
```

This creates a file like `cvat_backup_20260401.sql`. Copy it to your university shared drive:

```bash
cp cvat_backup_$(date +%Y%m%d).sql /path/to/your/shared/drive/
```

#### Restoring from a backup

```bash
cd ~/cvat
docker exec -i cvat_db psql -U root cvat < cvat_backup_20260401.sql
```

Replace `20260401` with the date of the backup file you want to restore.

#### Backup schedule summary

| What | How | When |
|------|-----|------|
| Completed tasks | Export as COCO 1.0 zip → save to shared drive | When each task reaches Acceptance |
| All annotations | Project-level COCO export → shared drive | Weekly |
| Full server (accounts + all data) | `pg_dump` SQL file → shared drive | Weekly |

---

## Next Step

- [Troubleshooting](../troubleshooting.md)
