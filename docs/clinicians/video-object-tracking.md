# Video Object Tracking

The tracking tool lets you draw (or accept from SAM) an annotation on **one frame**, and then the AI automatically follows that object through all the subsequent frames — so you don't have to adjust it manually on every frame.

> **Before you start:** Check that the tracking tool is available — click the **magic wand icon (✦)** in the left panel and look for a **Trackers** tab. If it is missing, contact your study coordinator.

---

## How Tracking Works

1. You have an annotation on a starting frame (either drawn manually or created with SAM).
2. You activate the tracker.
3. The AI follows the object forward, placing an adjusted annotation on every subsequent frame automatically.
4. You review the frames — on most frames the tracker will be correct. You only need to fix the frames where it drifted.

Tracking works best when:
- The object is clearly visible and well-lit.
- The camera is not moving very quickly.
- The object does not become hidden behind other structures for long periods.

---

## Step-by-Step: How to Track an Object

### Step 1 — Have an annotation on the starting frame

You should already have a mask or bounding box on the first frame where the object appears. This can be:
- A mask you accepted from SAM (see [Using the AI Tool](using-segment-anything-model.md)), or
- A shape you drew manually.

### Step 2 — Open the AI tools panel

1. Click the **magic wand icon (✦)** in the left panel.
2. Click the **Trackers** tab.
3. Click the tracker model name (e.g. **TransT**) to select it.

### Step 3 — Start tracking

1. Make sure you are on the frame with your starting annotation.
2. Click the **Track** button in the AI tools panel.
3. CVAT sends this frame to the AI. The tracker will now generate annotations on subsequent frames as you advance.

### Step 4 — Step through the frames and check

Press **`F`** to advance one frame at a time. On each frame you will see the tracker's result:

- **Looks correct?** Press `F` again to continue.
- **Drifted (wrong position or size)?**
  1. Click and drag the annotation to the correct position.
  2. Resize it if needed by dragging the corner handles.
  3. Continue pressing `F` — the tracker picks up from your correction.

### Step 5 — When the object leaves the video

When the object is no longer visible:
1. Right-click the annotation.
2. Select **Outside the frame**.

This marks the track as finished from this frame onwards without deleting it.

---

## What If I Don't Have the Tracking Tool?

If the **Trackers** tab is missing or empty, the tracking model has not been set up on the server yet. Contact your study coordinator.

As a fallback, you can use **CVAT's built-in interpolation** (no AI required):

1. Draw the annotation on frame 1.
2. Jump forward 20–30 frames (use the timeline or type the frame number).
3. Move the annotation to where the object is now.
4. CVAT automatically fills in the frames in between.

This is less accurate than AI tracking but still much faster than adjusting every single frame manually.

---

## Tips for Difficult Videos

| Problem | What to do |
|---------|-----------|
| Camera moves very quickly | Track in short bursts of 10–15 frames; correct, then continue |
| Object goes partially off screen | Mark as "outside" when less than half is visible; start a new annotation when it comes back fully |
| Two similar objects near each other | Track one at a time; use the eye icon (right panel) to hide the other while you work |
| Object changes appearance (e.g. view angle changes) | Correct the annotation early — the tracker adapts from corrected keyframes |

---

## Reviewing Your Work

After tracking all objects in the video, review the whole thing:

1. Go back to frame 1 (type `1` in the frame counter and press Enter, or drag the timeline back).
2. Press the **Play button** to watch the video with your annotations overlaid.
3. Look for:
   - Masks that drift away from the object.
   - Gaps (frames where the annotation disappeared but the object is still visible).
   - Annotations on frames where the object is not there.
4. Fix any issues, then save: **`Ctrl + S`**.

---

## Next Step

- [Reviewing and Exporting Annotations](../coordinator/reviewing-and-exporting.md)
