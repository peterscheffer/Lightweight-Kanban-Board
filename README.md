# Kanban Board

A lightweight, zero-dependency Kanban board that runs entirely in your browser — no server, no sign-up, no install. Just open the HTML file and start organizing tasks.

![Kanban Board](https://img.shields.io/badge/zero--dependency-HTML%20%2B%20JS-blue) ![License](https://img.shields.io/badge/license-MIT-green)

---

## Features

- **Works offline** — a single HTML file, no internet connection required after download
- **Persistent storage** — tasks are saved in your browser's `localStorage` and survive page refreshes and browser restarts
- **Drag and drop** — move cards between columns by dragging
- **Tags** — colour-coded labels to categorize tasks
- **Edit and delete** — click any card to edit it, hover to reveal the delete button
- **Quick add** — add tasks from the header button or the "+ Add task" button at the bottom of any column

---

## Getting Started

1. Download `kanban.html`
2. Open it in any modern browser (Chrome, Firefox, Safari, Edge)
3. That's it — your board is ready

No build step, no dependencies, no server needed.

---

## Usage

### Adding a task

Click **+ New Task** in the top-right header, or the **+ Add task** button at the bottom of any column. Fill in:

- **Title** (required)
- **Description** (optional)
- **Column** — which stage to place the task in
- **Tags** — click any tag pill to select it; click again to deselect

### Editing a task

Click anywhere on a card to open the edit modal. Change any fields and click **Save Changes**.

### Deleting a task

Hover over a card to reveal the **×** button in the top-right corner of the card. Click it and confirm.

### Moving tasks between columns

Drag a card and drop it onto any column. The column highlights when you're hovering over a valid drop target.

---

## Customising Columns

Columns are defined in the `COLUMNS` array near the top of the `<script>` block:

```js
const COLUMNS = [
  { id: 'backlog',    title: 'Backlog',      color: '#9ba3af' },
  { id: 'todo',       title: 'To Do',        color: '#4c9ced' },
  { id: 'inprogress', title: 'In Progress',  color: '#f59e0b' },
  { id: 'review',     title: 'In Review',    color: '#a78bfa' },
  { id: 'done',       title: 'Done',         color: '#34d399' }
];
```

To **add a column**, append a new object to the array:

```js
{ id: 'blocked', title: 'Blocked', color: '#f87171' }
```

To **rename a column**, change its `title` value. The `id` is used internally — if you change an `id`, any tasks previously stored in that column will lose their column assignment.

To **remove a column**, delete its entry from the array. Tasks in that column will no longer appear on the board (they remain in storage but are effectively orphaned).

To **change a column's dot colour**, update the `color` hex value.

After editing, also update the `<select>` options in the modal HTML to match your column `id` values:

```html
<select id="taskColumn">
  <option value="backlog">Backlog</option>
  <option value="todo">To Do</option>
  <!-- add or remove options here to match your COLUMNS array -->
</select>
```

---

## Customising Tags

Tags are defined in the `TAGS` array:

```js
const TAGS = [
  { name: 'design',   class: 'tag-design'   },
  { name: 'frontend', class: 'tag-frontend' },
  { name: 'backend',  class: 'tag-backend'  },
  { name: 'bug',      class: 'tag-bug'      },
  { name: 'urgent',   class: 'tag-urgent'   },
  { name: 'feature',  class: 'tag-feature'  },
  { name: 'docs',     class: 'tag-docs'     }
];
```

Each tag needs a `name` (displayed as the label) and a `class` (for styling).

To **add a new tag**, add an entry to the array and a matching CSS rule in the `<style>` block:

```js
// In TAGS array:
{ name: 'infra', class: 'tag-infra' }
```

```css
/* In <style>: */
.tag-infra { background: #fef9c3; color: #713f12; }
```

To **remove a tag**, delete its entry from the array. Cards that already have that tag stored will simply not render that tag pill.

To **change a tag's colour**, update the `background` and `color` values in its CSS rule.

---

## Data Storage

Tasks are stored in your browser's **`localStorage`** under the key `kanban-tasks`. This means:

- Data persists across sessions as long as you use the same browser on the same device
- Clearing your browser's site data or cache will erase your tasks
- Data does not sync across devices or browsers
- Opening the file in a different browser starts with a fresh default board

### Exporting your data

Open your browser's developer console (F12), go to the **Console** tab, and run:

```js
copy(localStorage.getItem('kanban-tasks'))
```

This copies your tasks as JSON to your clipboard. Paste it somewhere safe to back it up.

### Restoring a backup

In the console, paste:

```js
localStorage.setItem('kanban-tasks', '<your JSON here>'); location.reload();
```

### Resetting to defaults

```js
localStorage.removeItem('kanban-tasks'); location.reload();
```

---

## Browser Compatibility

Works in any modern browser that supports the Drag and Drop API and `localStorage`:

- Chrome 60+
- Firefox 60+
- Safari 12+
- Edge 79+

---

## License

MIT — do whatever you like with it.
