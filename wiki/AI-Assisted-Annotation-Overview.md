# AI-Assisted Annotation — Overview

CVAT integrates several AI models that can dramatically reduce the time needed to annotate videos. This page explains what AI assistance is available and how it fits into your workflow.

---

## What AI Assistance Can Do

| AI Feature | What it does | Time saving |
|------------|-------------|-------------|
| **Segment Anything Model (SAM)** | Click on an object → AI instantly draws a precise mask or polygon around it | Very high — replaces manual polygon tracing |
| **Semi-automatic tracking** | Draw a box on frame 1 → AI tracks the object automatically through subsequent frames | Very high — replaces frame-by-frame manual adjustment |
| **Automatic detection** | AI scans the entire video and automatically places bounding boxes on detected objects | High — useful as a starting point for review |

---

## How AI Tools Work in CVAT

CVAT uses a framework called **Nuclio** to run AI models as background services. These models must be deployed on the server before annotators can use them. **Your administrator handles this setup** — see [Installing AI Models](Installing-AI-Models).

Once deployed, the AI tools appear in the **left panel of the annotation editor** under the "magic wand" icon (AI Tools / Auto Annotation).

---

## Three Modes of AI Assistance

### 1. Interactive Annotation (Interactors)

You guide the AI by clicking on the object:
- Place **positive clicks** (left click) on the object you want to segment.
- Place **negative clicks** (right click or shift+click) on areas to exclude.
- The AI generates a segmentation mask in real time.
- Accept the result or refine it with more clicks.

**Models:** Segment Anything Model (SAM) — see [Using Segment Anything Model](Using-Segment-Anything-Model).

### 2. Semi-Automatic Tracking (Trackers)

Draw a bounding box around an object on one frame, then let the AI follow it through the video:
- Draw the initial bounding box.
- Click **Track** — the AI propagates the annotation forward through subsequent frames.
- Review and correct any frames where tracking drifts.

**Models:** TransT (Transformer Tracking) — see [Video Object Tracking](Video-Object-Tracking).

### 3. Automatic Detection (Detectors)

Run an AI detector across all frames of the task:
- No manual input required — the AI scans every frame.
- Results appear as automatically generated annotations.
- You then review and correct them.

> **Note for clinical annotation:** Automatic detectors (YOLO, Faster-RCNN etc.) are trained on general datasets and will not detect clinical-specific objects (polyps, instruments in endoscopy) reliably unless the model has been trained on your data. SAM and tracking are more immediately useful for clinical annotation because they require no prior training on your specific data.

---

## Recommended AI-Assisted Workflow for Clinical Videos

For most clinical video annotation tasks, the following combined workflow is most efficient:

```
For each object in the video:
  1. Navigate to the first frame where the object appears
  2. Use SAM (interactive) to click and instantly generate a precise segmentation
  3. Accept the SAM result → it creates a track annotation
  4. Use the Tracker to propagate the annotation forward through the video
  5. Review each frame — correct any frames where tracking drifted
  6. Mark the track as "outside" when the object leaves the video
  7. Save (Ctrl + S)
```

This approach combines the precision of SAM segmentation with the speed of automatic tracking, typically achieving a **5–10× reduction** in annotation time compared to fully manual frame-by-frame annotation.

---

## Prerequisites

Before you can use AI tools:

- The server administrator must have deployed the AI models (see [Installing AI Models](Installing-AI-Models)).
- You can verify that models are available by clicking the **magic wand icon** in the left panel of the annotation editor — if models are listed there, they are ready to use.
- If no models appear, contact your administrator.

---

## Next Steps

- [Installing AI Models (Nuclio + SAM)](Installing-AI-Models) — for administrators
- [Using Segment Anything Model (SAM)](Using-Segment-Anything-Model) — for annotators
- [Video Object Tracking](Video-Object-Tracking) — for annotators
