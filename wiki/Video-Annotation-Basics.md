# Video Annotation Basics

This page explains the core workflow for annotating a video in CVAT. Read this before using any AI tools.

---

## Opening Your Assigned Task

1. Log in to CVAT.
2. Click **Tasks** in the top navigation bar.
3. Find your task (it should have your name in the **Assignee** column).
4. Click **Open** (or click the task name).
5. Click the **Job** link to open the annotation editor.

---

## Understanding Tracks vs Shapes

For video annotation you can create:

| Type | Description | When to use |
|------|-------------|-------------|
| **Shape** | A single annotation on one frame only | For objects that appear in only one or a few frames |
| **Track** | An annotation that follows an object across multiple frames | For objects that persist through the video — **this is the main method for video annotation** |

> **For clinical video annotation, always use Tracks** unless specifically told otherwise. Tracks allow CVAT to link your annotation on frame 1 to the same object on frame 100, maintaining a consistent identity for each object throughout the video.

---

## Creating Your First Track

1. In the left panel, make sure the **Draw rectangle** tool is selected (press `R`), or choose a polygon/mask tool.
2. At the top of the left panel, ensure the mode is set to **Track** (not Shape). Look for a toggle near the top of the drawing tools.
3. Select the correct **label** from the label dropdown in the left panel.
4. **Click and drag** on the video canvas to draw a bounding box around the object.
5. Release the mouse. The annotation appears as a coloured box with the label name.
6. The track is now created. As you move to subsequent frames, this track continues and can be adjusted.

### Switching Between Track and Shape Mode

Near the drawing tools in the left panel you will see a toggle:
- **Shape** — annotation exists only on the current frame
- **Track** — annotation is linked across frames

Use the **Track** option for video annotation of persistent objects.

---

## Navigating Frames and Adjusting Annotations

Once you have created a track, move through the video frame by frame and adjust the annotation position as the object moves.

### Frame-by-Frame Workflow

1. **Draw the annotation** on the first frame where the object appears.
2. Press **`F`** to move to the next frame.
3. The annotation carries forward automatically.
4. If the object has moved, **click and drag** the annotation to its new position, or drag the corner handles to resize.
5. Press `F` again for the next frame.
6. Repeat until the object disappears from view.

### When an Object Leaves the Frame

When a tracked object disappears from the video:

1. Navigate to the frame where the object is last visible.
2. Right-click the annotation shape on the canvas (or click the object in the right panel Objects list).
3. Select **Outside the frame** — this marks the track as hidden from this frame onwards without deleting it.

Alternatively, if you used tracking (see [Video Object Tracking](Video-Object-Tracking)), the AI will handle this automatically.

---

## Interpolation — Automatic Frame Filling

CVAT can **automatically interpolate** the position of a tracked annotation between keyframes. This means:

1. Draw the annotation on frame 1 (a keyframe is created automatically).
2. Jump to frame 20 and move the annotation to where the object is now.
3. CVAT will automatically calculate the in-between positions for frames 2–19.

Interpolated frames are shown with a slightly different appearance in the timeline. You can always add more keyframes on any individual frame to refine the path.

**How to add a keyframe manually:**

- Right-click the shape and select **Make keyframe**, or
- Move the shape on any frame — CVAT automatically makes it a keyframe when you edit it.

---

## Editing Existing Annotations

- **Move a shape:** Click and drag the shape to a new position.
- **Resize:** Drag the corner handles of the shape.
- **Delete a shape on one frame:** Select it and press `Delete`. For tracks, this removes the annotation from the current frame only.
- **Delete an entire track:** Right-click the shape → **Remove track** (removes the annotation from all frames).
- **Change the label:** Select the shape, then change the label in the right panel.
- **Add attributes:** Select the shape; the attribute fields appear in the right panel. Fill them in.

---

## Saving Annotations

CVAT does **not** auto-save. Save your work regularly:

- Click the **Save** button in the top bar, or
- Press **`Ctrl + S`**

You will see a brief green notification confirming the save. Aim to save every 10–15 frames or whenever you finish annotating a significant section.

---

## Marking a Job as Complete

When you have finished annotating your assigned job:

1. Save your annotations (`Ctrl + S`).
2. Click the **Menu** button (top-right of the annotation editor, the three-bar icon or "hamburger" menu).
3. Select **Finish the job** (or similar — the exact label depends on the CVAT version).

Alternatively, the project lead can change the job stage from **Annotation** to **Validation** from the task management view.

---

## Common Mistakes to Avoid

| Mistake | How to avoid it |
|---------|-----------------|
| Using Shape mode instead of Track for persistent objects | Always check the Shape/Track toggle before drawing |
| Forgetting to save | Press `Ctrl + S` every 10–15 frames |
| Drawing on the wrong label | Check the selected label in the left panel before drawing |
| Annotating the wrong frame | Always check the frame number counter before drawing |
| Not marking objects as "outside" when they leave frame | Right-click → Outside the frame when object disappears |

---

## Next Step

- [Annotation Types](Annotation-Types) — learn which shape type to use for different structures
- [AI-Assisted Annotation — Overview](AI-Assisted-Annotation-Overview) — speed up your workflow with AI tools
