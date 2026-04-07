# Interface Overview

This page gives you a quick tour of the CVAT screen so you feel confident before you start annotating.

---

## The Main Dashboard

After logging in, you land on the main dashboard. Click **Tasks** in the top bar to find your assigned video.

```
┌──────────────────────────────────────────────────┐
│  CVAT  │  Projects   Tasks   Jobs            👤  │  ← top bar
├──────────────────────────────────────────────────┤
│                                                  │
│   Your assigned tasks appear here                │
│                                                  │
└──────────────────────────────────────────────────┘
```

| Item | What it is |
|------|-----------|
| **Tasks** | Click here to find your video to annotate |
| **Jobs** | If a task is split into sections, each section is a "job" |
| **👤 (top right)** | Your account — click to change your password or switch organisation |

---

## The Annotation Editor

When you open a task and click on a job, you enter the annotation editor. This is where you draw your masks.

```
┌──────────────────────────────────────────────────────────────┐
│  Save  Undo  Redo  ← Frame 42 of 300 →              Menu ≡  │ ← top bar
├─────────┬────────────────────────────────┬───────────────────┤
│         │                                │                   │
│  TOOLS  │                                │  OBJECTS LIST     │
│  (left) │                                │  (right)          │
│         │     VIDEO FRAME                │                   │
│  Draw   │     (the image you annotate)   │  Shows everything │
│  shapes │                                │  you have drawn   │
│         │                                │  on this frame    │
├─────────┴────────────────────────────────┴───────────────────┤
│  ◀◀  ◀  ▶  ▶▶    ────────── Timeline ──────────────────────  │ ← timeline
└──────────────────────────────────────────────────────────────┘
```

---

## The Tools Panel (Left Side)

These are the drawing tools. For this project you will mostly use the **Brush (mask)** tool and the **AI tool**.

| Tool | Keyboard key | What it does |
|------|-------------|-------------|
| **Arrow / Select** | `Esc` | Click to select or move an existing annotation |
| **Brush (mask)** | `B` | Paint a precise mask over an object — **use this for annotating** |
| **AI tool (magic wand ✦)** | — | Let the AI draw the mask for you with one click |
| **Rectangle** | `R` | Draw a rough bounding box (less common) |
| **Polygon** | `N` | Trace an outline by clicking around the edge |
| **Tag** | — | Label the whole frame (e.g. "poor visibility") without drawing a shape |

---

## The Objects Panel (Right Side)

This panel lists every annotation you have drawn on the current frame.

- **Click** any item in the list to select that annotation on the canvas.
- **Eye icon** — hide an annotation temporarily while you work on others.
- **Label name** — shown next to each object (e.g. "polyp").

---

## The Timeline (Bottom)

The timeline shows the full length of the video. Use it to move between frames.

| Button / Key | What it does |
|-------------|-------------|
| `F` | Go to the **next** frame |
| `D` | Go to the **previous** frame |
| `◀` / `▶` buttons | Step one frame back or forward |
| `◀◀` / `▶▶` buttons | Jump several frames |
| ▶ Play button | Play the video (no annotating while playing) |
| Frame counter (e.g. "42 / 300") | Shows which frame you are on |

Frames that already have annotations are shown as coloured marks on the timeline bar.

---

## Saving Your Work

> **CVAT does not save automatically.** You must save manually.

- Press **`Ctrl + S`** (Windows/Linux) or **`Cmd + S`** (Mac), or
- Click the **Save** button in the top bar.

A brief green message will confirm the save. **Save every 5–10 frames** to avoid losing work.

---

## Essential Keyboard Shortcuts

| Key | What it does |
|-----|-------------|
| `Ctrl + S` | **Save** your annotations |
| `Ctrl + Z` | **Undo** the last action |
| `F` | Next frame |
| `D` | Previous frame |
| `B` | Activate the brush/mask tool |
| `Esc` | Cancel what you are drawing / go back to select mode |
| `Delete` | Delete the selected annotation |
| `+` / `-` | Zoom in / zoom out on the image |
| `?` | Show all keyboard shortcuts |

---

## Next Step

- [Video Annotation Basics](video-annotation-basics.md) — start annotating
