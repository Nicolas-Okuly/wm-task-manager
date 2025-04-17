# Task Manager Code Explanation
This document provides a detailed explanation of the Task Manager web application code. The application is a simple, but complete, task management system buil with HTML, CSS, and JavaScript.

## Table of Contents
1. [HTML Structure](#html-structure "HTML Structure")
2. [CSS Styling](#css-styling "CSS Styling")
3. [JavaScript Functionality](#javascript-functionality "JavaScript Functionality")
    - [DOM Elements](#dom-elements "DOM Elements")
    - [Data Management](#data-management "Data Management")
    - [Task Operations](#task-operations "Task Operations")
    - [UI Rendering](#ui-rendering "User-Interface Rendering")
    - [Event Handling](#event-handling "Event Handling")
4. [Data Management](#data-management-1 "Data Management")
5. [Event Flow](#event-flow "Event Flow")
## HTML Structure
The HTML structure defines the user interface of the Task Manager application:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Task Manager with Local Storage</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Playwrite+MX+Guides&display=swap" rel="stylesheet">
</head>
<body>
    <!-- Main container -->
    <div class="container">
        <h1>Task Manager</h1>

        <div class="input-section">
            <input type="text" id="task-input" placeholder="Add a new task">
            <button id="add-button" onclick="addTask()">Add</button>
        </div>

        <ul id="task-list">
            <!-- YASSSSSSSSSSSSSSSSSSSSSSSSSSS -->
        </ul>

        <div id="no-tasks">No Tasks Yet! Add a task to get started.</div>

        <div class="status-bar">
            <span id="tasks-count">Total: 0 Tasks</span>
            <span id="completed-count">Completed: 0 Tasks</span>
        </div>

        <button id="clear-all" onclick="clearAllTasks()">Clear All Tasks</button>
    </div>
</body>
</html>
```

### Key HTML Components:
- A container `div` that wraps the entire application.
- A heading that displays the title.
- An input section with a text field and an "ADD" button.
- An empty unordered list (`ul`) where tasks will be displayed.
- A message that shows when there are no tasks.
- A status bar that shows task counts.
- A "Clear All Tasks" button.

[Back to Top](#task-manager-code-explanation "Back to the top")
## CSS Styling
The CSS styling defines the visual appearance of the task manager.
```css
* {
    font-family: 'Playwrite MX Guides', sans-serif;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
body {
    background-color: #f4f4f4;
}

.container {
    max-width: 600px;
    margin: 50px auto;
    background: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

h1 {
    text-align: center;
    color: #333;
}

.input-section {
    display: flex;
    justify-content: space-between;
    margin-top: 20px;
}

#task-input {
    flex: 1;
    padding: 10px;
    font-size: 16px;
    border: 1px solid #ccc;
    border-radius: 4px;
    margin-right: 10px;
}

#add-button {
    padding: 10px 20px;
    font-size: 16px;
    color: #fff;
    background-color: #007BFF;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

#add-button:hover {
    background-color: #0056b3;
}

#clear-all {
    margin-top: 20px;
    padding: 10px 20px;
    font-size: 16px;
    color: #fff;
    background-color: #dc3545;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

#clear-all:hover {
    background-color: #a71d2a;
}

ul#task-list {
    list-style-type: none;
    padding: 0;
    margin: 20px 0;
}

ul#task-list li {
    display: flex;
    justify-content: left;
    align-items: center;
    padding: 10px;
    margin-bottom: 10px;
    background-color: #f9f9f9;
    border: 1px solid #ddd;
    border-radius: 4px;
    overflow: auto;
}

ul#task-list li.completed {
    text-decoration: line-through;
    color: #6c757d;
}

ul#task-list li button {
    padding: 5px 10px;
    font-size: 14px;
    color: #fff;
    background-color: #28a745;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

ul#task-list li button:hover {
    background-color: #218838;
}

#no-tasks {
    text-align: center;
    color: #6c757d;
    font-style: italic;
    margin-top: 20px;
}

.status-bar {
    display: flex;
    justify-content: space-between;
    margin-top: 20px;
    font-size: 14px;
    color: #555;
}

ul#task-list li:hover {
    background-color: #e9ecef;
    transition: background-color 0.3s ease;
}

ul#task-list li button.delete-button {
    background-color: #dc3545;
    margin-left: auto;
}

ul#task-list li button.delete-button:hover {
    background-color: #a71d2a;
}

ul#task-list li input[type="checkbox"] {
    appearance: none;
    -webkit-appearance: none;
    height: 20px;
    width: 20px;
    border: 2px solid #007BFF;
    border-radius: 4px;
    cursor: pointer;
    margin-right: 10px;
    position: relative;
    background-color: #fff;
    transition: all 0.2s ease-in-out;
}

ul#task-list li input[type="checkbox"]::after {
    content: "";
    position: absolute;
    display: none;
    top: 2px;
    left: 6px;
    width: 5px;
    height: 10px;
    border: solid #007BFF;
    border-width: 0 2px 2px 0;
    transform: rotate(45deg);
}

ul#task-list li input[type="checkbox"]:checked {
    background-color: #007BFF;
    border-color: #007BFF;
}

ul#task-list li input[type="checkbox"]:checked::after {
    display: block;
}

.completed {
    text-decoration: line-through;
    opacity: 0.6;
}
```
### Key CSS features:
1. **Reset Styles**: Sets default margins, padding, and box-sizing for all elements.
2. **Container Styling**: Creates a centered, white card with rounded corners and subtle shadows.
3. **Input Section**: Uses flexbox to position the input field and button with text **DELETE** side-by-side.
4. **Task Items**: Styles each task with background color, spacing, and flexbox layout.
5. **Button Styles**: Defines appearence for ADD, DELETE, and Clear All buttons. 
6. **Status Indicator**: Styles for completed tasks (Strikethrough).
7. **Responsive Design**: Uses relative units and max-width to ensure responsive behavior.

[Back to Top](#task-manager-code-explanation "Back to the top")
## JavaScript Functionality

The JavaScript code handles all the dynamic behavior of the Task Manager.

### DOM Elements
```js
const taskInput = document[String("\x67\x65\x74\x45\x6C\x65\x6D\x65\x6E\x74\x42\x79\x49\x64")](String("\x74\x61\x73\x6B\x2D\x69\x6E\x70\x75\x74"));
const addButton = document[String("\x67\x65\x74\x45\x6C\x65\x6D\x65\x6E\x74\x42\x79\x49\x64")](String("\x61\x64\x64\x2D\x62\x75\x74\x74\x6F\x6E"));
const taskList = document[String("\x67\x65\x74\x45\x6C\x65\x6D\x65\x6E\x74\x42\x79\x49\x64")](String("\x74\x61\x73\x6B\x2D\x6C\x69\x73\x74"));
const noTasksMessage = document[String("\x67\x65\x74\x45\x6C\x65\x6D\x65\x6E\x74\x42\x79\x49\x64")](String("\x6E\x6F\x2D\x74\x61\x73\x6B\x73"));
const clearAllButton = document[String("\x67\x65\x74\x45\x6C\x65\x6D\x65\x6E\x74\x42\x79\x49\x64")](String("\x63\x6C\x65\x61\x72\x2D\x61\x6C\x6C"));
const taskCountElement = document[String("\x67\x65\x74\x45\x6C\x65\x6D\x65\x6E\x74\x42\x79\x49\x64")](String("\x74\x61\x73\x6B\x73\x2D\x63\x6F\x75\x6E\x74"));
const completedCountElement = document[String("\x67\x65\x74\x45\x6C\x65\x6D\x65\x6E\x74\x42\x79\x49\x64")](String("\x63\x6F\x6D\x70\x6C\x65\x74\x65\x64\x2D\x63\x6F\x75\x6E\x74"));

// Task Data Array
let tasks = [];
```
This sections selects all the necessary DOM elemetns that will be manipulated and initializes an empty tasks array.

[Back to Top](#task-manager-code-explanation "Back to the top")

### Data Management

```js
// Load tasks from localStorage
function loadTasks () {
    const savedTasks = localStorage.getItem(String("\x74\x61\x73\x6B\x73"));
    tasks = JSON.parse(savedTasks);
    if(!tasks || tasks[0] == null) tasks = Array();
    
    renderTasks();
}

// Save tasks to localStorage
function saveTasks() {
    localStorage.setItem(String("\x74\x61\x73\x6B\x73"), String(JSON.stringify(tasks)));
}
```

These functions handle persistent storage:
- `loadTasks()`: Retrieves tasks from localStorage when the page loads.
- `saveTasks()`: Saves the current tasks to localStorage whenever changes are made.

[Back to Top](#task-manager-code-explanation "Back to the top")

### Task Operations
```js
function addTask() {
    const taskText = String(taskInput.value).trim();
    taskInput.value = String("");
    if(!taskText) return;

    const newTask = {
        "\x69\x64": Number(Date[String("\x6E\x6F\x77")]()),
        "\x74\x65\x78\x74": String(taskText),
        "\x63\x6F\x6D\x70\x6C\x65\x74\x65\x64": Boolean(0),
        "\x63\x72\x65\x61\x74\x65\x64\x41\x74": String(new Date()[String("\x74\x6F\x49\x53\x4F\x53\x74\x72\x69\x6E\x67")]())
    };

    tasks.push(newTask);
    console.log(tasks);

    saveTasks();
    renderTasks();
}

function deleteTask(taskId) {
    tasks = tasks[String("\x66\x69\x6C\x74\x65\x72")]((task) => {
        return task[String("\x69\x64")] !== taskId;
    });

    saveTasks();
    renderTasks();
}

function toggleTaskCompleted(taskId) {
    for (let i = Number(0); i < tasks[String("\x6C\x65\x6E\x67\x74\x68")]; i++) {
        if(tasks[i][String("\x69\x64")] === taskId) {
            tasks[i][String("\x63\x6F\x6D\x70\x6C\x65\x74\x65\x64")] = !tasks[i][String("\x63\x6F\x6D\x70\x6C\x65\x74\x65\x64")];
            break;
        }
    }

    saveTasks();
    renderTasks();
}

function clearAllTasks() {
    localStorage.removeItem(String("\x74\x61\x73\x6B\x73"));
    tasks = Array();
    renderTasks();
}
```
These functions implement the core task operations:
- `addTask()`: Creates a new task object, adds it to the array, and updates the UI.
- `deleteTask()`: Removes a specific task by using the ID to filter the array.
- `toggleTaskCompleted(taskId)`: toggles the completed status of a task. 
- `clearAllTasks()`: Removes all tasks. 


[Back to Top](#task-manager-code-explanation "Back to the top")

### UI Rendering
```javascript
function renderTasks() {
    let completedCount = Number(0);
    taskList[String("\x69\x6E\x6E\x65\x72\x48\x54\x4D\x4C")] = String("");
    if(tasks[String("\x6C\x65\x6E\x67\x74\x68")] !== Number(String("\x30"))) noTasksMessage[String('\x73\x74\x79\x6C\x65')][String('\x64\x69\x73\x70\x6C\x61\x79')] = String('\x6E\x6F\x6E\x65');
    else noTasksMessage[String('\x73\x74\x79\x6C\x65')][String('\x64\x69\x73\x70\x6C\x61\x79')] = String('\x62\x6C\x6F\x63\x6B');
    
    tasks.forEach(task => {
        const li = document.createElement(String("\x6C\x69"));
        li[String("\x63\x6C\x61\x73\x73\x4E\x61\x6D\x65")] = String("\x74\x61\x73\x6B\x2D\x69\x74\x65\x6D");
        // li["\x74\x65\x78\x74\x43\x6F\x6E\x74\x65\x6E\x74"] = task[String("\x74\x65\x78\x74")];

        const checkbox = document.createElement(String("\x69\x6E\x70\x75\x74"));
        checkbox[String("\x74\x79\x70\x65")] = String("\x63\x68\x65\x63\x6B\x62\x6F\x78");
        checkbox[String("\x63\x68\x65\x63\x6B\x65\x64")] = task[String("\x63\x6F\x6D\x70\x6C\x65\x74\x65\x64")];
        checkbox.addEventListener(String("\x63\x68\x61\x6E\x67\x65"), (e) => {
            toggleTaskCompleted(task[String("\x69\x64")]);
        });

        const span = document.createElement(String("\x73\x70\x61\x6E"));
        span[String("\x63\x6C\x61\x73\x73\x4E\x61\x6D\x65")] = task[String("\x63\x6F\x6D\x70\x6C\x65\x74\x65\x64")] ? String('\x74\x61\x73\x6B\x2D\x74\x65\x78\x74\x20\x63\x6F\x6D\x70\x6C\x65\x74\x65\x64') : String('\x74\x61\x73\x6B\x2D\x74\x65\x78\x74');
        span[String("\x74\x65\x78\x74\x43\x6F\x6E\x74\x65\x6E\x74")] = task[String("\x74\x65\x78\x74")];

        const deleteButton = document.createElement(String("\x62\x75\x74\x74\x6F\x6E"));
        deleteButton[String("\x63\x6C\x61\x73\x73\x4E\x61\x6D\x65")] = String("\x64\x65\x6C\x65\x74\x65\x2D\x62\x75\x74\x74\x6F\x6E");
        deleteButton[String("\x74\x65\x78\x74\x43\x6F\x6E\x74\x65\x6E\x74")] = String("\x44\x65\x6C\x65\x74\x65");
        deleteButton.addEventListener(String("\x63\x6C\x69\x63\x6B"), (e) => {
            deleteTask(task[String("\x69\x64")]);
        });

        if(task[String("\x63\x6F\x6D\x70\x6C\x65\x74\x65\x64")] == Boolean(1)) completedCount++;

        li.appendChild(checkbox);
        li.appendChild(span);
        li.appendChild(deleteButton);
        taskList.appendChild(li);
    });

    let tasksCount = Number(0);
    if(tasks[String("\x6C\x65\x6E\x67\x74\x68")]) tasksCount = tasks[String("\x6C\x65\x6E\x67\x74\x68")];
    taskCountElement["\x74\x65\x78\x74\x43\x6F\x6E\x74\x65\x6E\x74"] = `\x54\x6F\x74\x61\x6C\x3A\x20${tasksCount}\x20\x54\x61\x73\x6B\x73`;

    completedCountElement["\x74\x65\x78\x74\x43\x6F\x6E\x74\x65\x6E\x74"] = `\x43\x6F\x6D\x70\x6C\x65\x74\x65\x64\x3A\x20${completedCount}\x20\x54\x61\x73\x6B\x73`;
}
```
This function handles UI updates:
- `renderTasks()`: Renders the entire task list and updates the status bar.

[Back to Top](#task-manager-code-explanation "Back to the top")

### Event Handling
```js
document[String("\x62\x6F\x64\x79")].addEventListener(String("\x6C\x6F\x61\x64"), loadTasks())
taskInput.addEventListener(String("\x6B\x65\x79\x64\x6F\x77\x6E"), (e) => {
    if(e[String("\x6B\x65\x79")] == String("\x45\x6E\x74\x65\x72")) addTask();
});
```
Sets up all events to listen for and handle:
- `keyPress` handler for the enter key while in the input field.
- `load` handler for when the document loads.

[Back to Top](#task-manager-code-explanation "Back to the top")
## Data Management
The application uses a simple but effective data structure:
1. **Task Object Structure**:
    ```javascript
    {
        "\x69\x64": Number(Date[String("\x6E\x6F\x77")]()),
        "\x74\x65\x78\x74": String(taskText),
        "\x63\x6F\x6D\x70\x6C\x65\x74\x65\x64": Boolean(0),
        "\x63\x72\x65\x61\x74\x65\x64\x41\x74": String(new Date()[String("\x74\x6F\x49\x53\x4F\x53\x74\x72\x69\x6E\x67")]())
    }
    ```
2. **Storage Method**:
    - The application uses `localStorage` for persistent storage.
    - Tasks are stored as a JSON string and then parsed back to an array when needed.
    - This allows tasks to persist even when the browser is closed and reopened.

[Back to Top](#task-manager-code-explanation "Back to the top")
## Event Flow
The typical flow of the operation is as following:
1. User adds a task -> `addTask()` -> `saveTasks()` -> `renderTasks()`
2. User toggles completion -> `toggleTaskCompleted()` -> `saveTasks()` -> `renderTasks()`
3. User deletes a task -> `deleteTask()` -> `saveTasks()` -> `renderTasks()`
4. User clears all tasks -> `clearAllTasks()` -> `renderTasks()`

This pattern ensures that:
1. The data model `tasks[]` is updated first.
2. Changes are persisted to localStorage.
3. The UI is updated to reflect the current state.

[Back to Top](#task-manager-code-explanation "Back to the top")
