## HTML Structure (planner.html)

The HTML file creates the basic structure of our planner:

```html
<!DOCTYPE html>
<html lang="en">
```
- This declares that we're writing an HTML5 document in English.

### Main Components:

1. **Calendar Section**:
   - Contains a header with navigation buttons (< and >)
   - Shows weekday names (Sun through Sat)
   - Has a grid for displaying dates and tasks

2. **Task Input Section**:
   - Text input for task description
   - DateTime input for selecting date and time
   - Add button to create new tasks

3. **Task List Section**:
   - Shows all added tasks
   - Each task can be marked as complete or deleted

## JavaScript Functionality (script.js)

### 1. Initial Setup
```javascript
const taskInput = document.getElementById('input-box');
const dateTimeInput = document.getElementById('datetime-input');
const listContainer = document.getElementById('list-container');
const calendar = document.getElementById('calendar');
```
- These lines connect our JavaScript to the HTML elements
- `getElementById` finds elements with matching ID attributes

### 2. Calendar Navigation
```javascript
let currentDate = new Date();
let selectedMonth = currentDate.getMonth();
let selectedYear = currentDate.getFullYear();
```
- Keeps track of which month/year is being displayed
- `currentDate` gets today's date
- `selectedMonth` and `selectedYear` track which month is shown

### 3. Calendar Rendering
```javascript
function renderCalendar() {
    // Creates the calendar view for the current month
    const firstDay = new Date(selectedYear, selectedMonth, 1);
    const lastDay = new Date(selectedYear, selectedMonth + 1, 0);
```
- `renderCalendar` creates the visual calendar
- Calculates first and last days of the month
- Creates day cells for each date

### 4. Task Management

#### Adding Tasks:
```javascript
function addTask() {
    const task = taskInput.value.trim();
    const datetime = dateTimeInput.value;
```
- Gets task text and chosen date/time
- Creates a new task element
- Adds it to both the list and calendar
- Saves to localStorage for persistence

#### Completing Tasks:
```javascript
li.addEventListener('click', function(e) {
    if (e.target.tagName !== 'BUTTON') {
        li.classList.toggle('completed');
        saveData();
        updateTasksOnCalendar();
    }
});
```
- Click a task to toggle completion
- Updates both list and calendar view
- Saves the new state

#### Removing Tasks:
```javascript
function removeTask(element) {
    element.remove();
    saveData();
    updateTasksOnCalendar();
}
```
- Deletes a task
- Updates storage and calendar

### 5. Data Persistence
```javascript
function saveData() {
    localStorage.setItem("tasks", listContainer.innerHTML);
}

function showTask() {
    listContainer.innerHTML = localStorage.getItem("tasks") || "";
}
```
- `saveData`: Saves tasks to browser storage
- `showTask`: Loads saved tasks when page opens

## CSS Styling (style.css)

### 1. Overall Layout
```css
body {
    background: linear-gradient(135deg, #74ABE2, #5563DE);
}

.container {
    display: grid;
    grid-template-columns: 1fr 1fr;
}
```
- Creates gradient background
- Uses CSS Grid for two-column layout

### 2. Calendar Styling
```css
.calendar-day {
    aspect-ratio: 1;
    padding: 5px;
    border: 1px solid #ddd;
}

.task-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
}
```
- Makes calendar cells square
- Creates circular dots for tasks

### 3. Task List Styling
```css
li {
    background: #fff;
    margin: 10px 0;
    padding: 10px;
    border-radius: 8px;
}

li.completed {
    text-decoration: line-through;
    color: gray;
}
```
- Styles individual task items
- Shows completed tasks with strikethrough
