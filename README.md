# 📅 College Event Calendar — DSA Project

A fully interactive **College Event Calendar** built as a single-page web application using **HTML, CSS, and JavaScript**. This project demonstrates core **Data Structures and Algorithms** concepts in a real-world scenario — scheduling college events while handling time conflicts using Arrays, Insertion Sort, Stacks, and Queues.

---

## 📌 Table of Contents

- [About the Project](#about-the-project)
- [Features](#features)
- [DSA Concepts Implemented](#dsa-concepts-implemented)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
- [How to Run](#how-to-run)
- [UI Overview](#ui-overview)
- [Sample Events (Pre-loaded)](#sample-events-pre-loaded)

---

## 📖 About the Project

The **College Event Calendar** is a web-based event scheduler that applies fundamental DSA concepts to solve the real-world problem of scheduling college events without time conflicts. When two events clash, the conflicting event is placed into a **waiting queue** and automatically scheduled as soon as a free slot becomes available. Deleted events are tracked on a **stack** to support undo functionality.

---

## ✨ Features

- **Add Events** — Schedule events with a title, start time, and end time
- **Conflict Detection** — Automatically detects overlapping events using interval overlap logic
- **Waiting Queue** — Conflicting events are placed in a FIFO queue and auto-scheduled when a slot opens
- **Delete Events** — Remove any scheduled event, triggering automatic queue processing
- **Undo Deletion** — Restore the last deleted event using a stack-based undo system
- **Auto-Queue Processing** — When an event is deleted, the waiting queue is immediately re-evaluated and events are promoted if their slot is now free
- **Live Statistics** — Real-time counts of scheduled events, total conflicts detected, and events in queue
- **Dark Mode** — Toggle between light and dark themes
- **Animations** — Smooth fade-in and slide-in animations for newly added or restored events
- **Responsive Design** — Adapts to both desktop and mobile screen sizes

---

## 🧩 DSA Concepts Implemented

| DSA Concept | Data Structure / Algorithm | How It's Used |
|---|---|---|
| **Array** | `events[]` | Stores all currently scheduled events |
| **Insertion Sort** | `insertionSortEvents()` | Keeps events sorted by start time after every addition |
| **Queue (FIFO)** | `waitingQueue[]` | Holds conflicting events in order; first-in, first-scheduled |
| **Stack (LIFO)** | `deletedStack[]` | Tracks deleted events for undo; last deleted is first restored |
| **Interval Overlap Check** | `eventsOverlap()` | Detects conflicts using: `startA < endB && startB < endA` |
| **Linear Search** | `findIndex()` | Locates an event by ID for deletion |
| **Greedy Processing** | `processWaitingQueue()` | After each deletion, scans the entire queue and schedules any now-conflict-free events |

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **HTML5** | Structure and layout of the single-page app |
| **CSS3** | Styling, dark mode, animations, responsive grid layout |
| **Vanilla JavaScript (ES6)** | All DSA logic and DOM manipulation |
| **Font Awesome 6** | Icons throughout the UI |

> No external JavaScript libraries or frameworks — all DSA logic is implemented from scratch.

---

## 📁 Project Structure

```
dsa-event-calendar/
└── DSA_event_calendar.html     # Complete single-file application
                                # (HTML + CSS + JavaScript in one file)
```

---

## ⚙️ How It Works

### Adding an Event
1. User enters a title, start time, and end time
2. The `hasConflict()` method checks all scheduled events for overlap using:
   ```
   startA < endB  AND  startB < endA
   ```
3. **No conflict** → Event is added to `events[]` and sorted using **Insertion Sort**
4. **Conflict detected** → Event is pushed to `waitingQueue[]` (shown in the Waiting Queue panel)

### Deleting an Event
1. The event is removed from `events[]` using `splice()`
2. It is immediately **pushed onto `deletedStack[]`** (enabling undo)
3. `processWaitingQueue()` is called — it scans every event in the queue and **promotes any that now have no conflict** into scheduled events
4. Promoted events are sorted back into `events[]` via Insertion Sort

### Undo Deletion
1. The most recently deleted event is **popped from `deletedStack[]`**
2. If restoring it causes no conflict → it is added back to `events[]`
3. If it would cause a conflict → it is moved to `waitingQueue[]` instead

### Queue Auto-Processing
After every deletion or undo, `processWaitingQueue()` iterates through the entire waiting queue. Events are greedily promoted whenever their time slot is free — simulating an **auto-scheduling system**.

---

## ▶️ How to Run

Since this is a completely self-contained single HTML file, no setup is needed.

1. Download `DSA_event_calendar.html`
2. Open it directly in any modern browser (Chrome, Firefox, Edge)

That's it — no server, no dependencies, no installation required.

---

## 🖥️ UI Overview

| Panel | Description |
|---|---|
| **Add New Event** (left) | Form to input event title, start time, end time |
| **DSA Concepts in Action** | Visual legend showing which DSA concepts are active |
| **Scheduled Events** (right) | Live list of all conflict-free events, sorted by time |
| **Stats Bar** | Shows count of scheduled events, conflicts found, and queue size |
| **Waiting Queue** (bottom-left) | Events that conflicted and are waiting for a free slot |
| **Deleted Events Stack** (bottom-right) | Stack of deleted events available for undo |

---

## 🎓 Sample Events (Pre-loaded)

The app loads with 5 demo events on startup to illustrate the DSA features:

| Event | Status |
|---|---|
| Data Structures Lecture | ✅ Scheduled |
| Algorithms Lab | ✅ Scheduled |
| Computer Networks | ✅ Scheduled |
| Math Tutorial | ⏳ In Queue (conflicts with DS Lecture) |
| Physics Lab | ⏳ In Queue (conflicts with Algorithms Lab) |

Delete any scheduled event to watch Math Tutorial or Physics Lab automatically move from the queue to the schedule.

---

## 📄 License

This project was created for educational purposes as part of a Data Structures and Algorithums.
