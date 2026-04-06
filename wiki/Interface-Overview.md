# Interface Overview

This page introduces the main areas of the CVAT interface so you can navigate confidently before you start annotating.

---

## The Main Dashboard

After logging in you land on the **Projects and Tasks** dashboard.

```
┌──────────────────────────────────────────────────────┐
│  CVAT logo │ Projects  Tasks  Jobs  Models  Cloud   │  ← Top navigation bar
│                                          [Username ▼] │
├──────────────────────────────────────────────────────┤
│                                                      │
│   [+ Create project]   [Search / Filter]             │
│                                                      │
│   Project cards or task cards appear here            │
│                                                      │
└──────────────────────────────────────────────────────┘
```

| Area | Description |
|------|-------------|
| **Projects** | Groups of related tasks. Think of a project as one study or one procedure type. |
| **Tasks** | Individual annotation jobs within a project. Each task usually corresponds to one video. |
| **Jobs** | Sub-divisions of a task. Large tasks may be split across multiple annotators. |
| **Models** | Lists the AI models deployed on the server (Segment Anything Model, tracking models, etc.). |
| **Cloud Storages** | Optional — for connecting cloud data sources. |

---

## The Annotation Editor

When you open a task and click **Open in editor** (or click a Job), you enter the annotation workspace.

```
┌─────────────────────────────────────────────────────────────────────┐
│  [Save]  [Undo]  [Redo]  [←Frame]  Frame: 42/300  [Frame→]  [Menu] │  ← Top bar
├─────────┬───────────────────────────────────────────┬───────────────┤
│         │                                           │               │
│  LEFT   │                                           │    RIGHT      │
│  PANEL  │         VIDEO CANVAS                      │    PANEL      │
│         │      (the video frame)                    │               │
│  Tools  │                                           │  Objects list │
│  &      │                                           │  Labels       │
│  Labels │                                           │  Attributes   │
│         │                                           │               │
├─────────┴───────────────────────────────────────────┴───────────────┤
│  [◀◀] [◀] [▶] [▶▶]  ─────────────────────Timeline────────────────  │  ← Timeline
└─────────────────────────────────────────────────────────────────────┘
```

---

## Left Panel — Tools

The left sidebar contains the annotation tools. The key tools you will use are:

| Icon / Tool | Shortcut | What it does |
|-------------|----------|-------------|
| **Cursor** (select) | `Esc` | Select and move existing shapes |
| **Draw bounding box** | `R` | Draw a rectangle around an object |
| **Draw polygon** | `N` | Draw a free-form polygon outline |
| **Draw mask / brush** | `B` | Paint a pixel-level mask on an object |
| **Draw polyline** | `L` | Draw a connected line |
| **Draw points** | `P` | Place individual points (keypoints) |
| **AI Tools (magic wand)** | — | Access Segment Anything Model and other AI models |
| **Tag** | — | Apply a label to the whole frame (no shape drawn) |

---

## Right Panel — Objects and Labels

The right panel shows:

- **Objects list** — every annotation shape on the current frame, with their label names. You can click any object here to select it, or use the eye icon to hide it temporarily.
- **Labels** — the list of label categories configured for this task (e.g. "polyp", "instrument", "lesion").
- **Attributes** — additional properties attached to the selected shape (e.g. size, confidence, type).

---

## The Timeline (Video Navigation)

At the bottom of the screen, the **timeline** shows the full length of the video. Each vertical line represents a frame.

| Control | Action |
|---------|--------|
| Frame counter | Shows current frame number and total frames |
| `◀` / `▶` buttons | Step backward or forward one frame |
| `◀◀` / `▶▶` buttons | Jump multiple frames |
| Playback button | Play the video through at normal speed |
| Coloured segments on timeline | Indicate which frames have annotations |
| Right-click on timeline | Jump to a specific frame number |

**Keyboard shortcuts for navigation:**

| Key | Action |
|-----|--------|
| `D` | Previous frame |
| `F` | Next frame |
| `V` | Go to previous annotation |
| `B` | Go to next annotation (when not using brush tool) |

---

## Saving Your Work

CVAT **does not auto-save** by default. Save frequently using:

- The **Save** button in the top bar, or
- The keyboard shortcut **`Ctrl + S`**

A green notification will appear briefly to confirm the save.

---

## Keyboard Shortcuts Reference

You can view all keyboard shortcuts at any time by pressing **`?`** in the annotation editor, or going to the Menu → Keyboard shortcuts.

| Key | Action |
|-----|--------|
| `Ctrl + S` | Save annotations |
| `Ctrl + Z` | Undo |
| `Ctrl + Y` | Redo |
| `F` | Next frame |
| `D` | Previous frame |
| `R` | Draw bounding box |
| `N` | Draw polygon (click to add points, double-click or `N` again to close) |
| `Esc` | Cancel current drawing / switch to select mode |
| `Delete` | Delete selected shape |
| `+` / `-` | Zoom in / zoom out |
| `Shift + B` | Fit frame to screen |
| `T` | Lock/unlock selected shape |
| `H` | Hide/show selected shape |

---

## Next Step

- [Creating Projects and Tasks](Creating-Projects-and-Tasks)
