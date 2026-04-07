# Annotation Types

For this project, the primary annotation type is the **segmentation mask**. This section explains what a mask is, how to draw one, and briefly describes the other shape types that are available if needed.

---

## Why We Use Segmentation Masks

A segmentation mask paints over the exact pixels that make up a structure (e.g. a polyp, lesion, or instrument). This is the annotation format required for training deep learning segmentation models, and it gives the most precise boundary information for clinical analysis.

> **For this project: always annotate using the Mask (brush) tool unless your project lead specifies otherwise.**

---

## Mask (Brush Tool) — Primary Annotation Type

A mask paints directly on the pixels of the object, giving a pixel-precise outline.

**Keyboard shortcut:** `B`

**How to draw a mask:**

1. Press `B` or click the **brush icon** in the left panel.
2. Select the correct **label** (e.g. "polyp") from the label dropdown.
3. Make sure the mode at the top of the tool panel is set to **Track** (for video) — not Shape.
4. **Paint over the object** by clicking and dragging your mouse across it. The mask appears as a coloured overlay.
5. Adjust the **brush size** using the slider in the tool panel — use a larger brush for filling large areas and a smaller brush for fine edges.
6. If you accidentally painted outside the object, switch to the **Eraser** (within the same tool panel) and erase the unwanted area.
7. When done, click **Apply** (or press `N`) to confirm the mask.

**Tips for accurate masks:**

| Tip | Detail |
|-----|--------|
| Zoom in first | Press `+` or scroll the mouse wheel to zoom in before painting fine edges |
| Use eraser for edges | Paint slightly over the edge, then erase back to the exact boundary |
| Polygon fill shortcut | Instead of painting stroke by stroke, click the **polygon** option within the mask tool — trace an outline by clicking, then the tool fills the entire area automatically |
| Check the outline | After applying, zoom in around the edges to check for gaps or overspill |

---

## Other Available Shape Types

These are available in CVAT but are secondary to masks for this project. Use them only when instructed by the project lead.

### Bounding Box (Rectangle)

A rectangular box that roughly surrounds an object. Fast to draw but imprecise — does not capture the exact object shape.

**Keyboard shortcut:** `R`

**How to draw:** Click and drag across the object. Release to finish.

**Use when:** Quick rough localisation is sufficient, or the object is too small/fast-moving to mask accurately.

---

### Polygon

Trace the exact outline of an object by clicking to place corner points around its edge. More precise than a bounding box but less precise than a mask.

**Keyboard shortcut:** `N`

**How to draw:**
1. Press `N` and select the label and Track mode.
2. Click around the object's edge to place points.
3. Double-click (or press `N` again) to close and finish the polygon.

**Editing:** Click and drag any corner point to refine. Click on the edge between points and drag to add a new point.

**Use when:** A clean polygon outline is preferred over a painted mask for a particular structure.

---

### Tag (Frame-Level Label)

Applies a label to the whole frame without drawing any shape. Nothing is drawn on the canvas.

**How to apply:** Click the **tag icon** (flag) in the left panel, then select the label.

**Use when:**
- Marking a frame as having **poor image quality**, **motion blur**, or **artefacts**.
- Flagging frames that **need review**.
- Classifying the frame content overall (e.g. "retroflexion view").

---

### Other Shapes (Polyline, Points, Ellipse)

These are available in CVAT but are unlikely to be needed for this project. Contact the project lead if you believe one of these is required for a specific annotation task.

---

## Annotation Format for This Project

All annotations exported from this project will use **COCO format** — the standard format for training segmentation models. CVAT handles the conversion automatically when you export.

- **Masks** → exported as polygon contours or RLE-encoded masks in COCO JSON format.
- **Bounding boxes** → exported as bounding box annotations in COCO JSON format.

See [Reviewing and Exporting Annotations](../coordinator/reviewing-and-exporting.md) for export instructions.

---

## Next Step

- [AI-Assisted Annotation — Overview](ai-assisted-annotation-overview.md) — use AI to draw masks faster
