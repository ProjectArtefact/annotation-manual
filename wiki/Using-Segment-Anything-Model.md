# Using Segment Anything Model (SAM)

Segment Anything Model (SAM) is an AI from Meta that can segment — precisely outline — any object with just a few clicks. In CVAT, SAM acts as an **interactive annotator**: you click on an object, and SAM instantly draws a precise mask or polygon around it.

> **Prerequisite:** SAM must be deployed on the server. See [Installing AI Models](Installing-AI-Models). If you can see SAM listed when you click the magic wand icon, it is ready to use.

---

## What SAM Does

Instead of manually tracing the outline of every object frame by frame, you simply:

1. Click **once** (or a few times) on the object.
2. SAM generates a precise segmentation mask covering the entire object.
3. You accept it, and the mask becomes your annotation.

This typically reduces annotation time for complex shapes (lesions, polyps, instruments) from **minutes per frame to seconds**.

---

## Opening the SAM Tool

1. Open your task in the annotation editor.
2. Navigate to the frame where you want to annotate.
3. In the **left panel**, click the **magic wand icon** (AI Tools / Auto Annotation).
4. The AI tools panel will expand. Click the **Interactors** tab.
5. You should see **Segment Anything** (or `pth-facebookresearch-sam-vit-h`) in the list.
6. Click on it to activate it.

---

## Annotating with SAM — Step by Step

### Selecting the Label

Before clicking on the image, make sure you have selected the correct **label** (e.g. "polyp", "instrument") from the label dropdown at the top of the AI tools panel.

### Placing Positive Clicks

1. With SAM activated, **left-click** on the object you want to segment.
2. SAM will immediately generate a segmentation mask (shown as a shaded overlay on the object).
3. The first click often produces a good result. If not, add more clicks.

### Placing Negative Clicks (to exclude areas)

If SAM has included areas you don't want (e.g. background, adjacent structures):

1. Hold **`Alt`** (or right-click, depending on your CVAT version) and click on the area you want to exclude.
2. SAM will update the mask in real time to exclude that region.

### Accepting the Result

Once the mask looks correct:

1. Click **Accept** (or press `N`).
2. The mask becomes a permanent annotation on the current frame.
3. You are returned to the normal annotation mode.

### If the Result is Wrong — Starting Over

If the SAM result is completely wrong:

1. Click **Reset** to clear all clicks and start again.
2. Try clicking on a more central part of the object, or use multiple clicks to guide SAM.

---

## Tips for Best Results with Clinical Videos

| Tip | Details |
|-----|---------|
| **Click on the centre of the object** | SAM works best when the initial click is in the middle of the object, not on the edge |
| **Use 2–3 clicks for complex shapes** | For irregular structures, place multiple positive clicks at different parts of the object |
| **Exclude background with negative clicks** | If SAM includes surrounding tissue, use negative clicks (Alt+click) to refine |
| **SAM works on one frame at a time** | After accepting the annotation, use the tracking tool to propagate it across frames |
| **Zoom in for small objects** | Use `+` to zoom into the canvas before clicking — this gives SAM a larger target |
| **Poor quality frames** | SAM may struggle on frames with motion blur, specular highlights, or blood. Skip these frames and annotate manually if needed |

---

## Using SAM Output as a Starting Point for a Track

The typical workflow combining SAM with video tracking:

1. Navigate to the first frame where the object appears.
2. Use SAM to generate a precise mask.
3. Accept the result — this creates a **shape** annotation (not yet a track).
4. Right-click the accepted annotation.
5. Select **Convert to track** (if available) — this makes it a track so it can persist across frames.
6. Now use the **Tracker** tool to propagate it forward. See [Video Object Tracking](Video-Object-Tracking).

> In some CVAT versions, when using SAM in **Track** mode (check the toggle in the tools panel), the result is already created as a track annotation automatically.

---

## SAM Performance Expectations

| Hardware | Speed per click |
|----------|----------------|
| NVIDIA GPU (e.g. RTX 3080) | < 1 second |
| CPU only | 3–10 seconds |

If SAM is slow, check with your administrator whether the GPU version has been deployed.

---

## Comparing SAM Output Types

Depending on which version of SAM is deployed, the output may be a:

- **Mask** — pixel-level segmentation (most precise)
- **Polygon** — fitted polygon around the mask (good for downstream use)

Both types work in CVAT. Your project lead will specify which type is required for your study.

---

## Next Step

- [Video Object Tracking](Video-Object-Tracking) — propagate SAM annotations across video frames automatically
