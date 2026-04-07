# System Requirements

> **This page is for the study coordinator** who will be installing and running CVAT. Clinicians who are only annotating do not need to read this — you just need Google Chrome on your computer.

---

## The Computer Running CVAT (the "server")

This can be any computer that stays switched on while annotators are working. It does not need to be a dedicated server — a regular desktop or laptop works fine for small teams.

| What you need | Minimum | Ideal |
|---------------|---------|-------|
| **Memory (RAM)** | 8 GB | 16 GB or more |
| **Free disk space** | 50 GB | 200 GB+ (more if you have lots of videos) |
| **Processor (CPU)** | 4 cores | 8+ cores |
| **Operating system** | Windows 10, macOS, or Ubuntu Linux | Ubuntu 22.04 |
| **Internet** | Needed during installation only | Not needed afterwards |

### If you want to use the AI tools (recommended)

The AI segmentation tool (SAM) works on any computer but runs much faster with a graphics card (GPU):

| | Without a GPU | With an NVIDIA GPU |
|-|--------------|-------------------|
| **AI speed** | 3–10 seconds per click | Under 1 second per click |
| **GPU memory needed** | Not applicable | 8 GB or more |

If the computer does not have an NVIDIA GPU, the AI tools will still work — they will just be a bit slower.

---

## The Computers Used for Annotating (clinician workstations)

Clinicians do not install anything. They only need:

| Requirement | Details |
|-------------|---------|
| **Browser** | **Google Chrome** — this is the only browser that works with CVAT |
| **Screen** | 1920 × 1080 resolution or larger recommended |
| **Mouse** | A standard mouse; a scroll wheel helps for zooming |
| **Network** | Must be able to connect to the computer where CVAT is installed |

---

## Next Step

- [Installation](installation.md) — install CVAT on your computer
