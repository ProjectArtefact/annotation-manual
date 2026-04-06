# First Login and Setup

This page covers the initial configuration steps after CVAT is installed: logging in as the administrator, creating annotator accounts, and setting up your organisation.

---

## Logging in as Administrator

1. Open **Google Chrome** and navigate to your CVAT address (e.g. `http://localhost:8080` or `http://YOUR-SERVER-IP:8080`).
2. Enter the **username** and **password** you created during installation (the superuser account).
3. Click **Login**.

---

## Understanding User Roles

CVAT has the following user roles:

| Role | What they can do |
|------|----------------|
| **Superuser (Admin)** | Full access: manage users, view the admin panel, create organisations |
| **Organisation Owner** | Create and manage projects, tasks, and members within an organisation |
| **Organisation Maintainer** | Create projects and tasks; manage members |
| **Supervisor** | Create tasks and review annotations |
| **Worker** | Annotate tasks assigned to them |

For most clinical annotation setups, you will have one or two administrators and several annotators (Workers or Supervisors).

---

## Creating an Organisation

Organising your work under an **Organisation** allows you to manage multiple projects and control who has access to what.

1. Click your username/avatar in the **top-right corner**.
2. Select **Create organization**.
3. Fill in:
   - **Short name** — a brief identifier (e.g. `clinical-study-2026`)
   - **Full name** — a descriptive name (e.g. `Endoscopy Annotation Study 2026`)
   - **Description** *(optional)*
   - **Email / Phone / Location** *(optional)*
4. Click **Submit**.

You are now the owner of the organisation. All annotators should be invited into this organisation.

---

## Creating Annotator Accounts

### Option A — Annotators self-register

By default, CVAT allows new users to register themselves:

1. Share the CVAT URL with annotators (e.g. `http://YOUR-SERVER-IP:8080`).
2. Annotators click **Create an account** on the login page and fill in their details.
3. After registering, their account exists but **they have no permissions** until added to your organisation (see below).

### Option B — Administrator creates accounts

1. Go to `http://YOUR-SERVER-IP:8080/admin/` (the Django admin panel).
2. Log in with the superuser credentials.
3. Click **Users → Add user**.
4. Enter a username and password and click **Save**.
5. On the next page, fill in optional profile details and assign appropriate permissions.

---

## Inviting Users to Your Organisation

Once an annotator has a CVAT account, you need to invite them to your organisation:

1. Click your username in the top-right corner and select your organisation from the menu.
2. Click the organisation name to open the organisation settings.
3. Go to the **Members** tab.
4. Click **Invite members**.
5. Enter the annotator's **username or email address**.
6. Choose their **role** (Worker for annotators, Supervisor for team leads).
7. Click **Send invitation** (or **Add** if they already have an account on the same server).

Repeat for each annotator.

---

## Switching Between Organisations

If you are a member of multiple organisations (or working both personally and within an organisation):

1. Click your avatar/username in the top-right corner.
2. Under **Organization**, select the organisation you want to work in.
3. The page will reload and all projects/tasks shown will be scoped to that organisation.

---

## Setting a User as an Annotator (Assigning to Tasks)

After creating an organisation and inviting members, the project lead assigns specific tasks to specific annotators when creating or editing a task. See [Creating Projects and Tasks](Creating-Projects-and-Tasks) for details.

---

## Changing Your Password

1. Click your username/avatar in the top-right corner.
2. Select **Account settings**.
3. Go to the **Password** section.
4. Enter your current password and choose a new one.
5. Click **Save**.

---

## Next Step

- [Interface Overview](Interface-Overview) — learn your way around the CVAT interface before you start annotating.
