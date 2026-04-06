# Uploading Videos

This page explains how to upload video files into CVAT tasks.

---

## Supported Video Formats

CVAT accepts most common video formats, including:

- **MP4** (H.264 codec — recommended for best compatibility)
- **AVI**
- **MOV**
- **MKV**
- **WebM**

> **Recommendation:** If possible, export or convert your endoscopy/clinical videos to **MP4 with H.264 encoding** before uploading. This gives the best playback performance in CVAT. Videos recorded in proprietary formats (e.g. from endoscopy systems) may need to be converted first.

---

## Converting Videos (if needed)

If your video is in an incompatible format, use **FFmpeg** to convert it. Install FFmpeg:

```bash
# Ubuntu
sudo apt-get install ffmpeg

# macOS (with Homebrew)
brew install ffmpeg

# Windows: download from https://ffmpeg.org/download.html
```

Convert to MP4 (H.264):

```bash
ffmpeg -i input_video.avi -c:v libx264 -crf 23 -preset medium -c:a aac output_video.mp4
```

---

## Uploading a Video When Creating a Task

During task creation (see [Creating Projects and Tasks](Creating-Projects-and-Tasks)):

1. In the **Files** section of the new task form, click **+ Add files**.
2. Select **My computer** from the tabs.
3. Click **Choose files** and select your video file.
4. The file will upload. A progress bar shows the upload status.
5. Once uploaded, the file name appears in the list.
6. Continue filling in the task settings and click **Submit**.

> **Large files:** Uploading large videos may take several minutes depending on your network speed. Do not close the browser tab while uploading.

---

## Uploading from a Shared Network Drive

If your server has a shared network storage mounted, you can link to files directly without uploading them:

1. The server administrator must first configure the shared storage path in CVAT's Docker configuration (see the [official CVAT documentation](https://docs.cvat.ai) for share path setup).
2. When creating a task, in the Files section, select the **Connected file share** tab.
3. Browse to and select your video file.

This is useful for large video libraries — it avoids re-uploading data that already exists on the server.

---

## Recommended Upload Settings for Clinical Videos

When creating the task after uploading, these settings are recommended for clinical video annotation:

| Setting | Recommended value | Reason |
|---------|------------------|--------|
| **Image quality** | 70–80% | Balances quality with storage and performance |
| **Overlap** | 0 | No overlap needed for sequential video annotation |
| **Segment size** | 0 (whole video in one job) or 500 for long videos | Split only if multiple annotators will work on the same video |
| **Frame step** | 1 | Annotate every frame for clinical accuracy |
| **Start frame** | 0 | Unless you only want to annotate a clip |
| **Stop frame** | (leave blank) | Annotate to the end of the video |

---

## Checking Your Upload

After task creation, verify the video was processed correctly:

1. Open the task by clicking its name.
2. Click on the **Job** that was created.
3. The annotation editor will open. You should see the first frame of your video in the canvas.
4. Use the timeline at the bottom to scrub through the video and confirm it plays correctly.

If the canvas shows an error or a blank frame, the video format may not be supported. Convert to MP4 (H.264) and re-upload.

---

## Deleting a Task

If you need to remove a task (e.g. uploaded the wrong video):

1. On the Tasks page, find the task.
2. Click the three-dot menu (`⋮`) next to the task.
3. Select **Delete**.
4. Confirm the deletion.

> **Warning:** Deleting a task permanently removes all annotations within it. This cannot be undone.

---

## Next Step

- [Video Annotation Basics](Video-Annotation-Basics)
