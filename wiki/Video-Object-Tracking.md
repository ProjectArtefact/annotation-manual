# Video Object Tracking

Object tracking in CVAT allows you to draw or accept an annotation on **one frame** and have the AI automatically follow that object through all subsequent frames. This eliminates the need to manually adjust annotations on every single frame.

> **Prerequisite:** A tracking model (e.g. TransT) must be deployed on the server. See [Installing AI Models](Installing-AI-Models). If you can see tracking models in the AI tools panel, they are ready.

---

## How Tracking Works

1. You provide an initial annotation (bounding box or mask) on a starting frame.
2. The tracker analyses the object's appearance and position.
3. It automatically generates annotations on subsequent frames by following the object.
4. You review the results and correct any frames where the tracker drifted.

Tracking is most reliable when:
- The object is clearly visible with good contrast against the background.
- The object does not move too rapidly between frames.
- The object is not occluded for long periods.

---

## Method 1 — Using the AI Tracker Tool (Recommended)

This is the primary method for video annotation with AI assistance.

### Step 1 — Open the AI Tools Panel

1. In the annotation editor, click the **magic wand icon** in the left panel.
2. Click the **Trackers** tab (next to Interactors).
3. Select **TransT** (or whichever tracker model is available).

### Step 2 — Draw the Initial Bounding Box

1. Make sure you are on the first frame where the object appears.
2. Select the correct **label** in the tools panel.
3. **Click and drag** on the canvas to draw a bounding box tightly around the object.
4. Release the mouse.

### Step 3 — Start Tracking

1. Click the **Track** button in the AI tools panel.
2. CVAT will send the current frame and bounding box to the tracking model.
3. The model will process the subsequent frames. You will see the annotations being generated automatically as you advance through frames.

> **Note:** The tracker runs frame-by-frame in the background. You advance through frames manually (press `F`) and the tracker generates the next frame's annotation as you go.

### Step 4 — Review and Correct

Advance through the video frame by frame (`F` key):
- If the tracker result looks correct, move to the next frame.
- If the tracker has drifted (the box is in the wrong position or size):
  1. Click and drag the box to the correct position.
  2. Resize as needed by dragging the corner handles.
  3. Continue pressing `F` — the tracker resets from this corrected keyframe.

### Step 5 — Stop Tracking

When the object leaves the frame or tracking is complete:
1. Right-click the annotation.
2. Select **Outside the frame** to mark the track as invisible from this frame onwards.

---

## Method 2 — Semi-Automatic Tracking via Existing Annotations

If you have already created track annotations (e.g. using SAM) and want to propagate them:

1. Select an existing track annotation (click it).
2. Open the AI tools panel → **Trackers** tab.
3. Select the tracker model.
4. Click **Track** — the model will use the current shape as the starting point and follow it forward.

---

## Method 3 — Propagate (Interpolation Only, No AI)

If no tracking model is deployed, CVAT can still interpolate between keyframes without AI:

1. Draw the annotation on the first keyframe.
2. Advance to a later frame (e.g. 30 frames later).
3. Adjust the annotation to the object's new position.
4. CVAT automatically **interpolates** all frames in between.

This is less accurate than AI tracking but requires no additional setup.

---

## Tracking Tips for Clinical Videos

| Situation | Recommendation |
|-----------|---------------|
| Fast camera movement | Track in shorter segments (every 10–15 frames), then correct manually |
| Object partially out of frame | Mark as "outside" when < 50% visible; re-annotate when fully visible again |
| Multiple similar objects | Track one object at a time; use distinct colours/labels for each |
| Specular highlights overlapping object | The tracker may drift. Correct manually on affected frames |
| Object appearance changes (e.g. polyp view angle changes) | Add a corrective keyframe early — the tracker will learn the new appearance |
| Video with frequent camera reinsertion | Treat each insertion as a separate scene; start a new track after each gap |

---

## Managing Multiple Tracks

For videos with multiple objects to annotate simultaneously:

1. Annotate and track **one object at a time** to avoid confusion.
2. Use a different label and colour for each object type.
3. After tracking all instances of one object type, move on to the next.
4. The Objects panel on the right shows all active tracks — use the eye icon to hide tracks temporarily while working on others.

---

## Reviewing Tracking Results

After tracking, review your work efficiently:

1. Go back to frame 1.
2. Press the **Play** button to watch the video with your annotations overlaid.
3. Watch for:
   - Tracks that drift away from the object.
   - Tracks that disappear prematurely.
   - Incorrect frame ranges (object visible but annotation missing, or annotation present on frames where object is not visible).
4. Correct any issues, then save (`Ctrl + S`).

---

## Keyboard Shortcuts for Tracking Workflow

| Key | Action |
|-----|--------|
| `F` | Advance one frame forward |
| `D` | Go back one frame |
| `Ctrl + S` | Save annotations |
| `V` | Jump to the previous annotated frame |
| `B` | Jump to the next annotated frame (when not in brush mode) |
| `Delete` | Remove annotation from current frame only |

---

## Next Step

- [Reviewing and Exporting Annotations](Reviewing-and-Exporting)
