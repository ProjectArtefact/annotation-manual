# AI-Assisted Annotation — Overview

CVAT includes AI tools that can dramatically reduce the time it takes to annotate videos. Instead of carefully tracing every object by hand on every frame, the AI can do most of the drawing for you.

---

## What the AI Can Do

### 1. Draw the mask for you (Segment Anything Model — SAM)

You click once on a lesion or structure, and the AI instantly draws a precise mask around it. This replaces the need to trace outlines manually.

- **How to use it:** See [Using the AI Tool (SAM)](using-segment-anything-model.md)
- **Time saving:** What might take 1–2 minutes of careful tracing takes about 2 seconds.

### 2. Follow the object across frames (Object Tracking)

You draw (or accept) an annotation on one frame, and the AI automatically follows that object through the rest of the video — adjusting the annotation on every subsequent frame.

- **How to use it:** See [Video Object Tracking](video-object-tracking.md)
- **Time saving:** Instead of adjusting annotations on every frame manually, you just check and correct the few frames where the AI drifted.

---

## The Recommended Workflow

Combining both AI tools gives the fastest and most accurate results:

```
For each object in the video:

  1. Go to the first frame where it appears
  2. Click on it with the AI tool (SAM) → AI draws the mask
  3. Accept the mask → this creates your annotation
  4. Use the Tracker → AI follows the object forward through the video
  5. Step through frames and correct any where the AI drifted
  6. When the object leaves the video, mark it as "outside"
  7. Save (Ctrl + S)
```

This typically cuts annotation time by **5 to 10 times** compared to drawing every frame by hand.

---

## Before You Start — Check AI Tools Are Available

The AI tools must be set up by your study coordinator before you can use them. To check:

1. Open a task in the annotation editor.
2. Look in the **left panel** for the **magic wand icon (✦)**.
3. Click it — a panel should open showing available AI tools.
4. If the panel is empty or the icon is missing, contact your study coordinator at [ameya.pore@univr.it](mailto:ameya.pore@univr.it).

---

## Next Steps

- [Using the AI Tool (SAM)](using-segment-anything-model.md) — click to segment
- [Video Object Tracking](video-object-tracking.md) — follow objects across frames
- [Installing AI Models](../coordinator/installing-ai-models.md) — for the study coordinator setting up the AI
