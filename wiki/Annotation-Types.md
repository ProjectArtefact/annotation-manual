# Annotation Types

CVAT supports several types of annotation shapes. This page describes each type, how to draw it, and when to use it for clinical video annotation.

---

## Overview of Shape Types

| Shape | Keyboard shortcut | Best used for |
|-------|-------------------|---------------|
| **Bounding Box (Rectangle)** | `R` | Quickly marking the location of an object |
| **Polygon** | `N` | Precisely outlining irregular shapes (lesions, instruments) |
| **Mask (Brush)** | `B` | Pixel-level segmentation of structures |
| **Polyline** | `L` | Linear structures (e.g. guidewires, anatomy boundaries) |
| **Points** | `P` | Keypoint annotation (e.g. specific anatomical landmarks) |
| **Ellipse** | `E` | Circular or oval structures |
| **Tag** | — | Frame-level labels (no shape, e.g. "poor visibility", "artefact") |

---

## Bounding Box (Rectangle)

A rectangular box that roughly surrounds an object. This is the fastest shape to draw.

**How to draw:**
1. Press `R` (or click the rectangle tool in the left panel).
2. Make sure **Track** mode is selected for video.
3. Select the correct label.
4. Click and drag across the object on the canvas.
5. Release the mouse to finalise.

**When to use:**
- Initial quick annotation of object location
- When precise boundaries are not required
- For small or fast-moving objects where exact segmentation is impractical

---

## Polygon

A polygon allows you to trace the exact outline of an object by clicking to place vertices.

**How to draw:**
1. Press `N` (or click the polygon tool).
2. Select **Track** mode and the correct label.
3. Click to place the first point on the object's boundary.
4. Continue clicking around the outline to place vertices.
5. **Double-click** (or press `N` again) to close the polygon and finish.

**Editing a polygon after drawing:**
- Click the polygon to select it.
- Drag any existing vertex to a new position.
- Right-click on a vertex to delete it.
- Click on the polygon edge (between two vertices) and drag to add a new vertex.

**When to use:**
- Precise outlining of lesions, polyps, or anatomical structures
- When bounding boxes are too imprecise for your study requirements

---

## Mask (Brush Tool)

A mask paints over the object at the pixel level, giving the most precise annotation.

**How to draw:**
1. Press `B` (or click the brush/mask tool in the left panel).
2. Select the correct label.
3. Use the **brush** to paint over the object. Adjust the brush size with the slider in the tool options.
4. Use the **eraser** (within the same tool) to remove any areas you painted by mistake.
5. Click **Apply** or press `N` to finalise the mask.

**Modes within the brush tool:**
- **Brush** — paints inclusion of the mask
- **Eraser** — removes parts of the mask
- **Polygon fill** — click to trace a polygon and fill it as a mask

**When to use:**
- When you need pixel-accurate boundaries (e.g. for training segmentation models)
- For structures with complex, irregular boundaries
- When using the Segment Anything Model (SAM) — SAM outputs results as masks automatically

---

## Polyline

A connected line (not a closed shape).

**How to draw:**
1. Press `L` (or click the polyline tool).
2. Click to place points along the line.
3. Double-click to finish the polyline.

**When to use:**
- Linear anatomical structures (e.g. bowel wall, instrument shaft)
- Measurement lines

---

## Points (Keypoints)

Discrete points placed on specific locations.

**How to draw:**
1. Press `P` (or click the points tool).
2. Click on the image to place each point.
3. Press `N` or double-click to finish placing points for the current annotation.

**When to use:**
- Specific anatomical landmarks
- Centre-of-mass annotations

---

## Tag (Frame-Level Label)

A tag does not draw any shape — it applies a label to the entire frame. Useful for classifying frames.

**How to apply:**
1. Click the **Tag** tool (flag icon) in the left panel.
2. Select the label you want to apply to this frame.
3. The label is recorded but nothing is drawn on the canvas.

**When to use:**
- Marking frames with poor image quality, motion blur, or artefacts
- Classifying frame content (e.g. "retroflex view", "instrument present")
- Quality flags (e.g. "needs review")

---

## Choosing the Right Shape for Clinical Annotation

The following is general guidance — always defer to the specific annotation protocol for your study:

| Clinical structure | Recommended shape |
|-------------------|------------------|
| Polyp / lesion (rough location) | Bounding box |
| Polyp / lesion (precise boundary) | Polygon or Mask |
| Endoscope tip | Bounding box |
| Surgical instrument | Bounding box or Polygon |
| Anatomical region of interest | Polygon or Mask |
| Poor visibility / artefact frame | Tag |
| Guidewire / catheter | Polyline |
| Specific landmark | Points |

---

## Changing the Shape Type of an Existing Annotation

You can convert an existing annotation to a different shape type:

1. Right-click the annotation.
2. Select **Edit** → **Change shape type** (if available in your CVAT version).
3. Select the new type.

Note: not all conversions are available. In many cases it is easier to delete and re-annotate with the correct shape.

---

## Next Step

- [AI-Assisted Annotation — Overview](AI-Assisted-Annotation-Overview)
