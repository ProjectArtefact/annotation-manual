# Reviewing and Exporting Annotations

This page covers quality review of completed annotations and exporting the finished data for downstream use.

---

## Part 1 — Reviewing Annotations

### Who Reviews?

Typically the project lead, a senior annotator, or a designated reviewer checks completed work before it is accepted. In CVAT this is managed through **job stages**.

### Changing a Job Stage

1. From the **Tasks** page, click the task name.
2. You will see the list of jobs within the task.
3. Click on a job to expand its details.
4. Change the **Stage** dropdown:
   - `Annotation` → `Validation` (when the annotator has finished and the work is ready for review)
   - `Validation` → `Acceptance` (when the reviewer is satisfied)
   - `Validation` → `Annotation` (to send the job back to the annotator for corrections)
5. Click **Save**.

The annotator will see their job stage has changed when they next log in.

### Opening a Job for Review

1. As a reviewer, open the task and click the job.
2. The annotation editor opens as normal.
3. Use the timeline and frame navigation to step through all frames.
4. Check that:
   - All objects have been annotated on every frame they are visible.
   - Labels are correct.
   - Track boundaries (start and end frames) are accurate.
   - Masks/polygons accurately cover the objects.
   - Attributes (if required by the protocol) have been filled in.

### Leaving Feedback

Currently CVAT's community edition does not have a built-in comment/feedback tool per annotation. To communicate feedback to annotators:

- Use your team's standard communication channel (email, messaging app).
- Note the specific frame number, track ID, and the correction required.
- Alternatively, annotators can be given back the job (stage back to `Annotation`) and corrective annotations can be drawn on top of the existing ones for discussion.

### Quality Metrics (Optional)

CVAT supports **consensus jobs** and **ground truth jobs** for inter-annotator agreement scoring in more advanced setups. Consult the [CVAT documentation](https://docs.cvat.ai) for details on these features.

---

## Part 2 — Exporting Annotations

Once annotations are reviewed and accepted, export them for use in your research or model training pipeline.

### How to Export a Task

1. From the **Tasks** page, find your task.
2. Click the **three-dot menu** (`⋮`) next to the task.
3. Select **Export task dataset**.
4. Choose your **export format** (see below).
5. Check **Save images** if you also want the video frames saved alongside the annotations.
6. Click **OK** (or **Export**).
7. CVAT will prepare the export file. When ready, the file will download to your browser's default Downloads folder.

### Exporting a Single Job (Partial Export)

To export only the annotations from a specific job (e.g. one segment of a long video):

1. Open the task.
2. Click on the specific job.
3. In the annotation editor, go to **Menu** (top-right) → **Export job dataset**.
4. Choose your format and download.

---

## Export Formats

| Format | Best for | Notes |
|--------|---------|-------|
| **CVAT for video (XML)** | Sharing with other CVAT users; backup | Native CVAT format — preserves all track information |
| **COCO** | Machine learning training | JSON format; widely supported by ML frameworks |
| **Pascal VOC** | Object detection training | XML format per frame |
| **YOLO** | YOLO model training | Text files per frame |
| **Segmentation mask (PNG)** | Pixel-level analysis | Exports masks as grayscale or colour PNG images |
| **MOT (Multiple Object Tracking)** | Video tracking datasets | Text format with frame, ID, bounding box |
| **Datumaro** | CVAT's native ML format | Supports all annotation types |
| **VGGImage Annotator (VIA)** | Simple JSON format | Useful for simple downstream analysis |

> **Recommendation for clinical research:** Use **CVAT for video (XML)** as your primary backup/archive format, as it preserves all information. Use **COCO** or **MOT** if you need to pass annotations to an ML engineer.

---

## Re-Importing / Updating Annotations

If you need to update annotations after export (e.g. after an ML model has refined them):

1. From the task, click the three-dot menu → **Upload annotations**.
2. Select the format and upload the annotation file.
3. Choose whether to **merge** with existing annotations or **replace** them.

---

## Backing Up Your Data

It is important to back up both the CVAT database and your exported annotation files regularly.

### Exporting All Tasks at Once

For a full backup, export each task individually using the process above. Store the exported files in a secure location separate from the CVAT server.

### Database Backup (Administrator)

The CVAT database can be backed up by copying the Docker volume:

```bash
# Backup the PostgreSQL database
docker exec cvat_db pg_dump -U root cvat > cvat_backup_$(date +%Y%m%d).sql
```

Store this SQL file securely. To restore:

```bash
docker exec -i cvat_db psql -U root cvat < cvat_backup_YYYYMMDD.sql
```

---

## Annotation Checklist Before Export

Before marking a job as accepted and exporting, run through this checklist:

- [ ] All objects annotated on every frame they are visible
- [ ] Tracks start on the correct first frame and end on the correct last frame
- [ ] Objects marked as "outside" on frames where they are not visible
- [ ] All required attributes filled in for each annotation
- [ ] Labels are correct (no mislabelled objects)
- [ ] Annotations saved (`Ctrl + S`)
- [ ] Job stage set to `Acceptance`

---

## Next Step

- [Troubleshooting](Troubleshooting) — if you encounter any issues
