
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List Manager</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }
        .container {
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            width: 400px;
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .task-input {
            display: flex;
            justify-content: space-between;
            margin-bottom: 20px;
        }
        .task-input input[type="text"] {
            width: 75%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .task-input button {
            padding: 10px;
            background-color: #4A90E2;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .task-input button:hover {
            background-color: #357ABD;
        }
        ul {
            list-style-type: none;
            padding: 0;
        }
        li {
            background: #f9f9f9;
            margin: 10px 0;
            padding: 15px;
            display: flex;
            justify-content: space-between;
            border-radius: 5px;
            border: 1px solid #ddd;
        }
        .task-buttons {
            display: flex;
            gap: 10px;
        }
        .task-buttons button {
            padding: 5px;
            border: none;
            cursor: pointer;
            border-radius: 3px;
        }
        .edit {
            background-color: #FFD700;
            color: white;
        }
        .edit:hover {
            background-color: #E6C200;
        }
        .delete {
            background-color: #FF6347;
            color: white;
        }
        .delete:hover {
            background-color: #E65342;
        }
        .completed {
            text-decoration: line-through;
            color: gray;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>To-Do List</h1>
    
    <div class="task-input">
        <input type="text" id="task-input" placeholder="Enter a new task">
        <button onclick="addTask()">Add Task</button>
    </div>
    
    <ul id="task-list"></ul>
</div>

<script>
    // Add a new task
    function addTask() {
        const taskInput = document.getElementById('task-input');
        const taskText = taskInput.value;

        if (taskText === '') {
            alert('Please enter a task.');
            return;
        }

        const taskList = document.getElementById('task-list');

        // Create new list item
        const listItem = document.createElement('li');

        // Create text element for task
        const taskElement = document.createElement('span');
        taskElement.innerText = taskText;
        
        // Create buttons for edit, complete, and delete
        const editButton = document.createElement('button');
        editButton.innerText = 'Edit';
        editButton.classList.add('edit');
        editButton.onclick = function() { editTask(taskElement); };

        const completeButton = document.createElement('button');
        completeButton.innerText = 'Complete';
        completeButton.classList.add('complete');
        completeButton.onclick = function() { toggleComplete(taskElement); };

        const deleteButton = document.createElement('button');
        deleteButton.innerText = 'Delete';
        deleteButton.classList.add('delete');
        deleteButton.onclick = function() { deleteTask(listItem); };

        // Add text and buttons to the list item
        listItem.appendChild(taskElement);
        const buttonContainer = document.createElement('div');
        buttonContainer.classList.add('task-buttons');
        buttonContainer.appendChild(editButton);
        buttonContainer.appendChild(completeButton);
        buttonContainer.appendChild(deleteButton);
        listItem.appendChild(buttonContainer);

        // Add list item to the task list
        taskList.appendChild(listItem);

        // Clear input
        taskInput.value = '';
    }

    // Edit a task
    function editTask(taskElement) {
        const newTaskText = prompt('Edit the task:', taskElement.innerText);
        if (newTaskText !== null && newTaskText !== '') {
            taskElement.innerText = newTaskText;
        }
    }

    // Mark a task as completed/incomplete
    function toggleComplete(taskElement) {
        taskElement.classList.toggle('completed');
    }

    // Delete a task
    function deleteTask(listItem) {
        if (confirm('Are you sure you want to delete this task?')) {
            listItem.remove();
        }
    }
</script>

</body>
</html>
