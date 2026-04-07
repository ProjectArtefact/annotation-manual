# Using the AI Tool (Segment Anything Model)

The AI segmentation tool — called **Segment Anything Model**, or SAM — lets you annotate an object with just one or two clicks. Instead of tracing the outline manually, you click on the object and the AI draws a precise mask around it instantly.

> **Before you start:** Check that the AI tool is available — click the **magic wand icon (✦)** in the left panel of the annotation editor. If nothing appears, contact your study coordinator.

---

## What SAM Does

1. You click on an object (e.g. a polyp).
2. SAM analyses the image and draws a mask around the object.
3. You review the mask — if it looks right, you accept it.
4. The mask becomes your annotation.

This takes **about 2 seconds** per frame instead of the 1–2 minutes it would take to trace the outline manually.

---

## Step-by-Step: How to Use SAM

### Step 1 — Open the AI tool

1. In the annotation editor, click the **magic wand icon (✦)** in the left panel.
2. A panel opens. Click the **Interactors** tab.
3. Click on **Segment Anything** in the list to activate it.

### Step 2 — Select the right label

At the top of the AI tools panel, make sure the correct **label** is selected (e.g. "polyp"). This is what your annotation will be called.

Also check that the mode is set to **Track** (not Shape), so the annotation persists across frames.

### Step 3 — Click on the object

**Left-click** on the object you want to annotate. SAM will immediately draw a coloured mask over it.

- Click in the **middle** of the object for the best result.
- If the first click gives a good result, move on to Step 4.
- If the mask is too big or too small, add more clicks on the parts of the object that were missed (see refinement tips below).

### Step 4 — Refine if needed

**If the mask includes areas you did not want** (e.g. surrounding tissue):
- Hold **`Alt`** and click on the unwanted area to remove it from the mask.

**If the mask is missing part of the object:**
- Left-click on the missed part to add it.

**If the result is completely wrong:**
- Click **Reset** to start again, then try clicking on a different part of the object.

### Step 5 — Accept the mask

Once the mask looks correct, click **Accept** (or press `N`).

The mask is now saved as an annotation on this frame. You are returned to the normal view.

---

## Tips for Best Results

| Situation | What to do |
|-----------|-----------|
| Small lesion | Zoom in first (press `+` or scroll the mouse wheel), then click |
| Irregular shape | Click 2–3 times at different points within the object |
| Mask spills onto surrounding tissue | Hold `Alt` and click on the spill area to remove it |
| Blurry or dark frame | Try clicking on the clearest part; if results are still poor, annotate this frame manually with the brush tool |
| Object very close to another structure | Use negative clicks (`Alt`+click) on the neighbouring structure to separate them |

---

## After Accepting — Propagate Across Frames

SAM annotates one frame at a time. Once you have accepted the mask on the first frame:

1. Use the **Tracking tool** to automatically follow the object across the rest of the video.
2. See [Video Object Tracking](video-object-tracking.md) for the next step.

---

## If SAM Is Slow

If SAM takes more than 5–10 seconds to respond after each click, let your study coordinator know. The AI tool runs faster with a dedicated graphics card (GPU) on the server.

---

## Next Step

- [Video Object Tracking](video-object-tracking.md) — follow the object across all frames automatically
