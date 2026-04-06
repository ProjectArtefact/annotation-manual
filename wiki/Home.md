# Video Annotation Manual — Home

Welcome to the clinical video annotation guide. This wiki walks you through every step required to set up and use **CVAT** (Computer Vision Annotation Tool) — including AI-assisted segmentation and automatic video tracking — so that you can annotate clinical video data efficiently and consistently.

---

## What is CVAT?

CVAT is a free, open-source annotation tool used by research teams worldwide to label images and videos with bounding boxes, polygons, masks, keypoints, and more. It runs locally on your organisation's server so your data never leaves your network, and it supports AI models that dramatically speed up the annotation process.

---

## How to Use This Wiki

Work through the pages in order the first time. Once you are set up, use the sidebar to jump directly to the section you need.

| Step | Page | Who needs it |
|------|------|-------------|
| 1 | [System Requirements](System-Requirements) | Everyone |
| 2 | [Installation — Ubuntu](Installation-Ubuntu) | Server administrator |
| 2 | [Installation — Windows](Installation-Windows) | Server administrator (Windows) |
| 2 | [Installation — macOS](Installation-macOS) | Server administrator (Mac) |
| 3 | [First Login and Setup](First-Login-and-Setup) | Administrator + all annotators |
| 4 | [Interface Overview](Interface-Overview) | All annotators |
| 5 | [Creating Projects and Tasks](Creating-Projects-and-Tasks) | Project lead / administrator |
| 6 | [Uploading Videos](Uploading-Videos) | Project lead / administrator |
| 7 | [Video Annotation Basics](Video-Annotation-Basics) | All annotators |
| 8 | [Annotation Types](Annotation-Types) | All annotators |
| 9 | [AI-Assisted Annotation — Overview](AI-Assisted-Annotation-Overview) | All annotators |
| 10 | [Installing AI Models (Nuclio + SAM)](Installing-AI-Models) | Server administrator |
| 11 | [Using Segment Anything Model (SAM)](Using-Segment-Anything-Model) | All annotators |
| 12 | [Video Object Tracking](Video-Object-Tracking) | All annotators |
| 13 | [Reviewing and Exporting Annotations](Reviewing-and-Exporting) | All annotators + project lead |
| 14 | [Troubleshooting](Troubleshooting) | Everyone |

---

## Quick Reference

- **CVAT runs in your browser** — use **Google Chrome** (the only fully supported browser).
- **Default address after installation:** `http://localhost:8080` (or your server's IP/hostname on port 8080).
- **Supported browsers:** Google Chrome only.
- **Video formats:** MP4, AVI, MOV, MKV, and most other common video formats.

---

## Getting Help

If something is not covered in this wiki, refer to the official CVAT documentation at [docs.cvat.ai](https://docs.cvat.ai) or raise an issue in the organisation's GitHub repository.
