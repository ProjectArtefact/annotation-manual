# Creating Projects and Tasks

Before annotators can start working, an administrator or project lead must create a **Project** (to group related work) and **Tasks** (one per video). Labels — the categories you will annotate — are defined at this stage.

---

## Projects vs Tasks vs Jobs

| Concept | Description | Example |
|---------|-------------|---------|
| **Project** | A collection of related annotation tasks | "Colonoscopy Polyp Study 2026" |
| **Task** | One annotation unit, usually one video | "Patient_001_video.mp4" |
| **Job** | A segment of a task, assigned to one annotator | Frames 0–150 of the above task |

Labels defined on a Project are inherited by all tasks within it, so you only need to define them once.

---

## Creating a Project

1. From the main dashboard, click **Projects** in the top navigation bar.
2. Click **+ Create a new project**.
3. Fill in the project details:
   - **Name** — e.g. `Colonoscopy Polyp Study 2026`
   - **Labels** — define your annotation categories (see below)
4. Click **Submit**.

### Defining Labels

Labels are the categories annotators will apply to objects in the video (e.g. "polyp", "instrument", "lesion").

For each label:

1. Click **Add label**.
2. Enter the label **name** (e.g. `polyp`).
3. Choose a **colour** — each label gets a distinct colour so shapes are visually distinguishable.
4. Add **attributes** if needed (optional — see below).
5. Click the tick/checkmark to confirm the label.
6. Repeat for all required labels.

#### Adding Attributes to Labels

Attributes allow annotators to record additional information about each annotation (e.g. polyp size category, morphology type).

1. On the label, click **Add attribute**.
2. Give the attribute a **name** (e.g. `morphology`).
3. Choose the **input type**:
   - **Select** — a dropdown list of options (e.g. pedunculated, sessile, flat)
   - **Text** — free text
   - **Number** — numeric value with min/max/step
   - **Checkbox** — yes/no toggle
4. For Select type, enter the **values** separated by Enter (one per line).
5. Check **Required** if annotators must fill this in before moving to the next frame.

---

## Creating a Task

1. From the main dashboard, click **Tasks** in the top navigation, then **+ Create new task**.  
   *Or*, open a project and click **+ Create new task** within it.

2. Fill in the task details:

   - **Name** — e.g. `Patient_001_20260401`
   - **Project** — select the project this task belongs to (labels are inherited automatically)
   - **Labels** — only needed if not using a project, or if you want to override the project labels
   - **Subset** — optional (train/test/validation split label — useful for ML teams)

3. Under **Files**, upload your video file. See [Uploading Videos](Uploading-Videos) for details.

4. Under **Advanced configuration** *(click to expand)*:
   - **Image quality** — leave at default (70%) unless you need full resolution
   - **Overlap size** — number of frames to overlap between job segments (leave at 0 for video annotation)
   - **Segment size** — how many frames per job segment. If you want to split a long video across multiple annotators, set this to e.g. 500 (frames per job)
   - **Start frame / Stop frame** — annotate only a portion of the video
   - **Frame step** — annotate every Nth frame (e.g. 5 = annotate every 5th frame). Leave at 1 to annotate every frame.

5. Click **Submit & Open**.

---

## Assigning an Annotator to a Job

After creating a task, CVAT automatically creates one or more **Jobs** within it (depending on segment size). Assign specific annotators to specific jobs:

1. Open the task by clicking its name.
2. You will see a list of **Jobs** (job segments).
3. Click on a job to expand it.
4. In the **Assignee** field, search for and select the annotator's username.
5. Set the **Stage** to `Annotation` (the default).
6. Click **Save**.

Repeat for each job segment.

---

## Task Stages

Each job moves through the following stages:

| Stage | Meaning |
|-------|---------|
| **Annotation** | The annotator is actively adding annotations |
| **Validation** | A reviewer is checking the annotations |
| **Acceptance** | The annotations have been reviewed and accepted |

Annotators can only edit jobs in the **Annotation** stage. The project lead or reviewer changes the stage after reviewing.

---

## Duplicating a Task

If you want to create a new task with the same labels and settings as an existing one:

1. On the Tasks page, find the task you want to duplicate.
2. Click the three-dot menu (`⋮`) next to it.
3. Select **Copy**.
4. Upload the new video file and adjust the name.
5. Click **Submit**.

---

## Next Step

- [Uploading Videos](Uploading-Videos)
