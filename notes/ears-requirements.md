# Exercise 1 — EARS requirements

**Goal (v2):** a web app that runs locally and shows the state of the tickets in every project folder under one root folder. The root folder is set by an environment variable.

**Definitions**

- **Root folder:** the folder named by the root-folder environment variable (for example `C:/VersionManagement`).
- **Ticket file:** a file named `IT-<number>[-<slug>].md`, for example `IT-658-session-names.md`.
- **Key:** the `IT-<number>` part of the file name, for example `IT-658`.
- **Title:** the `<slug>` part of the file name, for example `session-names`.
- **Known statuses:** `OPEN`, `IN DEVELOPMENT`, `READY FOR REVIEW`, `IN REVIEW`, `APPROVED`, `REJECTED`, `DONE`.

Subfolders are never scanned: only folders directly under the root folder, and only files directly in a `docs` folder.

---

## R1 — Event-driven

**When** the user opens the application, **the system shall** list, by name, every folder located directly under the root folder whose `docs` folder directly contains at least one ticket file.

**Test**
- Input: a root folder with `A/docs/IT-1-a.md`, `B/docs/notes.md`, `C/` with no `docs`, and `D/sub/docs/IT-2.md`.
- Action: open the application.
- Expected: the list shows `A` only.

## R2 — State-driven

**While** no folder is selected from the list, **the system shall** show a message asking the user to select a folder.

**Test**
- Input: the root folder from R1.
- Action: open the application and select nothing.
- Expected: the message asking to select a folder is shown, and no ticket is shown.

## R3 — Event-driven

**When** the user selects a folder from the list, **the system shall** show every ticket file located directly in that folder's `docs` folder, each with its key, its title and its status.

**Test**
- Input: `A/docs/IT-3-fix-login.md` with `**Status:** OPEN`, `A/docs/IT-4.md` with `**Status:** DONE`, and `A/docs/old/IT-5-x.md`.
- Action: select `A`.
- Expected: two tickets — `IT-3` · `fix-login` · `OPEN`, and `IT-4` · (no title) · `DONE`. `IT-5` is not shown.

## R4 — Unwanted behaviour

**If** a ticket file has no `**Status:**` line, or its value is not one of the known statuses, **then the system shall** show the ticket with the status `UNKNOWN` and shall not hide it.

**Test**
- Input: `A/docs/IT-6.md` with no status line, and `A/docs/IT-7.md` with `**Status:** WAITING`.
- Action: select `A`.
- Expected: both tickets are shown, each with the status `UNKNOWN`.
