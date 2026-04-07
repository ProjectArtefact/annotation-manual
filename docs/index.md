# Video Annotation Manual — Home

Welcome to the annotation guide for the endoscopy study.

---

## Important Notes

- **Data Privacy:** CVAT runs on a **dedicated university PC**. No patient data is uploaded to the internet.
- **What you will do:** Draw **segmentation masks** around lesion regions in endoscopy video frames.
- **Questions?** Contact [ameya.pore@univr.it](mailto:ameya.pore@univr.it)

---

## How This Study Is Set Up

```
University PC (running CVAT)
        │
        ├── Clinician A's laptop  ──── connects via SSH tunnel ──► Chrome → http://localhost:8080
        │
        └── Clinician B's laptop  ──── connects via SSH tunnel ──► Chrome → http://localhost:8080
```

- CVAT is installed **once** on a dedicated university PC by the study coordinator (Amey).
- Each clinician **connects to it from their own laptop** using an SSH tunnel — there is nothing to install.
- All annotation data is stored centrally on the university PC.

---

## Start Here — Which one are you?

### I am a clinician — I need to connect and start annotating

| Step | Page |
|------|------|
| 1 | [Connecting to CVAT via SSH](clinicians/clinician-workflow.md#what-is-the-ssh-tunnel) — first time setup |
| 2 | [Logging In](clinicians/clinician-workflow.md#logging-in-to-cvat) — your CVAT username and password |
| 3 | [Interface Overview](clinicians/interface-overview.md) — a tour of the screen |
| 4 | [Video Annotation Basics](clinicians/video-annotation-basics.md) — how to annotate your assigned task |
| 5 | [Annotation Types](clinicians/annotation-types.md) — what shapes to draw |
| 6 | [Using the AI Tool (SAM)](clinicians/using-segment-anything-model.md) — let AI draw the mask for you |
| 7 | [Video Object Tracking](clinicians/video-object-tracking.md) — let AI follow the object across frames |
| 8 | [Finishing Your Task](clinicians/clinician-workflow.md#finishing-your-annotation-task) — how to submit when done |
| 9 | [Reviewing Another Clinician's Work](clinicians/clinician-workflow.md#reviewing-another-clinicians-work) — how to act as a reviewer |
| — | [Troubleshooting](troubleshooting.md) — if something goes wrong |

---

### I am the study coordinator (Amey)

| Step | Page |
|------|------|
| 1 | [System Requirements](coordinator/system-requirements.md) |
| 2 | [Installation](coordinator/installation.md) — install CVAT on the university PC (done once) |
| 3 | [First Login and Setup](coordinator/first-login-and-setup.md) — create SSH accounts + CVAT accounts for clinicians |
| 4 | [Creating Projects and Tasks](coordinator/creating-projects-and-tasks.md) — set up the annotation work |
| 5 | [Uploading Videos](coordinator/uploading-videos.md) — add the endoscopy videos |
| 6 | [Installing AI Models](coordinator/installing-ai-models.md) — enable the AI annotation tools |
| 7 | [Reviewing and Exporting Annotations](coordinator/reviewing-and-exporting.md) — monitor progress and download finished data |

---

## Quick Reference

| Item | Details |
|------|---------|
| **Clinician connection** | SSH tunnel then open Chrome at `http://localhost:8080` |
| **Browser** | Google Chrome only |
| **Save your work** | `Ctrl + S` — CVAT does not auto-save |
| **Questions** | [ameya.pore@univr.it](mailto:ameya.pore@univr.it) |
