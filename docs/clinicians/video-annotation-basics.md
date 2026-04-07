# Video Annotation Basics

This page explains the core workflow for annotating a video. Read this before using the AI tools.

---

## Opening Your Task

1. Open **Google Chrome** and go to the CVAT address your study coordinator gave you.
2. Log in with your username and password.
3. Click **Tasks** in the top navigation bar.
4. Find your task — it should have your name next to it.
5. Click the task name, then click the **Job** link that appears.
6. The annotation editor opens with your video.

> **No tasks visible?** Check that you are in the right organisation — click your name (top-right) and look for the study name under "Organization". Click it to switch.

---

## Understanding the Two Annotation Modes

Before you start drawing, you need to understand the difference between a **Shape** and a **Track**:

| Mode | What it does |
|------|-------------|
| **Shape** | Draws an annotation on **this frame only** |
| **Track** | Draws an annotation that **follows the object through the whole video** |

> **Always use Track mode** for this study. This links your annotation across all frames so the same object is consistently labelled throughout the video.

You will see a **Shape / Track toggle** near the top of the drawing tools on the left side. Make sure **Track** is selected before you draw.

---

## The Basic Annotation Workflow

Here is the step-by-step process for annotating one object in a video:

**1. Go to the first frame where the object appears**

Use `D` (back) and `F` (forward) to navigate to the frame where the lesion or structure first becomes visible.

**2. Draw a mask around the object**

- Press `B` to activate the brush tool.
- Make sure the correct **label** is selected in the left panel (e.g. "polyp").
- Make sure **Track** is selected (not Shape).
- Paint over the object by clicking and dragging. The mask appears as a coloured overlay.

> **Tip: Use the AI tool instead of painting manually.** The AI can draw the mask for you with a single click. See [Using the AI Tool (SAM)](using-segment-anything-model.md).

**3. Confirm the annotation**

Click **Apply** or press `N` to confirm the mask.

**4. Move to the next frame**

Press `F` to go to the next frame. The annotation carries forward automatically.

**5. Adjust if the object has moved**

If the object has shifted position, drag the mask to its new location or repaint it. Each time you edit, CVAT records it as a new keyframe.

> **Tip: Use the AI tracking tool.** Instead of adjusting every frame manually, the AI can follow the object automatically. See [Video Object Tracking](video-object-tracking.md).

**6. When the object disappears from the video**

Right-click the annotation on the canvas, then select **Outside the frame**. This marks the track as hidden from this point onwards without deleting it.

**7. Save your work**

Press **`Ctrl + S`** regularly (every 5–10 frames). CVAT does not save automatically.

---

## Editing Annotations You Have Already Made

| What you want to do | How to do it |
|--------------------|-------------|
| Move a mask to a new position | Click and drag it |
| Make it bigger or smaller | Drag the edge handles |
| Fix the painted area | Press `B` to go back into brush mode; use the eraser to remove parts |
| Delete the annotation from this frame only | Select it and press `Delete` |
| Delete the annotation from all frames | Right-click it → **Remove track** |
| Change its label | Select it, then change the label in the right panel |

---

## When You Have Finished Your Task

1. Save your work one final time: **`Ctrl + S`**.
2. Click the **Menu** button (the three-bar icon ≡ in the top-right of the editor).
3. Select **Finish the job**.
4. Let your study coordinator know you have finished so they can review your work.

---

## Common Mistakes to Avoid

| Mistake | How to avoid it |
|---------|----------------|
| Using Shape mode instead of Track | Always check the Track toggle before drawing |
| Forgetting to save | Press `Ctrl + S` every 5–10 frames |
| Drawing with the wrong label selected | Check the label name in the left panel before painting |
| Not marking objects as "outside" when they leave the frame | Right-click → Outside the frame when the object disappears |

---

## Next Step

- [Annotation Types](annotation-types.md) — what shape to draw for different structures
- [Using the AI Tool (SAM)](using-segment-anything-model.md) — let AI draw the mask for you
