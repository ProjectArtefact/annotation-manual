# Uploading Videos

> **This is a one-time setup step** done by whoever created the project. If tasks have already been set up and assigned to you, skip this page and go to [Video Annotation Basics](../clinicians/video-annotation-basics.md).

---

## Supported Video Formats

CVAT works best with **MP4** files. It also accepts AVI, MOV, MKV, and WebM.

> **If your endoscopy system exports in a format other than MP4**, you will need to convert the file first (see below).

---

## How to Upload a Video

Videos are uploaded when you create a task (see [Creating Projects and Tasks](creating-projects-and-tasks.md)):

1. In the **Files** section of the new task form, click **+ Add files**.
2. Select the **My computer** tab.
3. Click **Choose files** and select your video.
4. A progress bar shows the upload. Wait for it to finish — do not close the browser tab.
5. Once uploaded, continue filling in the task settings and click **Submit**.

> **Large files:** Videos over 1 GB may take several minutes to upload. This is normal.

---

## If Your Video Format Is Not Supported

If CVAT shows a blank or broken frame after uploading, your video format may need converting to MP4.

**The easiest way is to use HandBrake — a free, simple desktop app:**

1. Download **HandBrake** from [handbrake.fr](https://handbrake.fr/) (available for Windows, Mac, and Linux — no terminal needed).
2. Open HandBrake and click **Open Source** — select your video file.
3. Under **Presets**, choose **Fast 1080p30** (or a similar preset).
4. Make sure the **Format** is set to **MP4**.
5. Click **Start Encode**.
6. Upload the converted MP4 file to CVAT.

---

## Recommended Settings When Creating the Task

When creating a task after uploading, these defaults work well for endoscopy video annotation:

| Setting | Recommended | Notes |
|---------|------------|-------|
| **Image quality** | 70% (default) | Leave as-is unless image detail is lost |
| **Frame step** | 1 | Annotate every frame |
| **Segment size** | 0 | Whole video in one job (change only if splitting across clinicians) |

---

## Checking the Video Loaded Correctly

After creating the task:

1. Open the task by clicking its name.
2. Click the **Job** link.
3. The annotation editor opens — you should see the first frame of the video on screen.
4. Press `F` a few times to step through several frames and confirm the video plays correctly.

If the screen is blank or shows an error, the video format is likely the issue — convert to MP4 using HandBrake and re-upload.

---

## Deleting a Task

If you uploaded the wrong video and need to start over:

1. On the Tasks page, click the **⋮ (three-dot menu)** next to the task.
2. Select **Delete**.
3. Confirm.

> Deleting a task permanently removes all its annotations. This cannot be undone.

---

## Next Step

- [Video Annotation Basics](../clinicians/video-annotation-basics.md) — share this with your clinicians
- [Installing AI Models](installing-ai-models.md) — set up the AI tools before clinicians start
