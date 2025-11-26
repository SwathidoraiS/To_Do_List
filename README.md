# Ex03 To-Do List using JavaScript
## Date:03/09/2025
## Name: Swathi S 
## Reg No: 212223040220

## AIM
To create a To-do Application with all features using JavaScript.

## ALGORITHM
### STEP 1
Build the HTML structure (index.html).

### STEP 2
Style the App (style.css).

### STEP 3
Plan the features the To-Do App should have.

### STEP 4
Create a To-do application using Javascript.

### STEP 5
Add functionalities.

### STEP 6
Test the App.

### STEP 7
Open the HTML file in a browser to check layout and functionality.

### STEP 8
Fix styling issues and refine content placement.

### STEP 9
Deploy the website.

### STEP 10
Upload to GitHub Pages for free hosting.

## PROGRAM
```
index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My To-Do App</title>
  <style>
    body {
      font-family: "Poppins", sans-serif;
      background: #0d0d0d; /* Black background */
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      color: #eee; /* Light text */
    }

    .todo-container {
      background: #1a1a1a; /* Dark card */
      padding: 30px;
      border-radius: 18px;
      width: 450px;
      box-shadow: 0 8px 25px rgba(125,60,255,0.4); /* Purple glow */
    }

    h1 {
      text-align: center;
      margin-bottom: 5px;
      font-size: 28px;
      color: #a259ff; /* Bright Purple */
      text-shadow: 0 0 10px rgba(162,89,255,0.8);
    }

    .subtitle {
      text-align: center;
      margin-bottom: 20px;
      color: #ccc;
      font-size: 14px;
    }

    .instructions {
      background: #262626;
      padding: 12px;
      border-radius: 10px;
      margin-bottom: 20px;
      font-size: 14px;
      color: #bbb;
    }

    .input-section {
      display: flex;
      gap: 10px;
    }

    input {
      flex: 1;
      padding: 12px;
      border-radius: 10px;
      border: 2px solid #333;
      font-size: 16px;
      outline: none;
      background: #0d0d0d;
      color: #fff;
      transition: 0.3s;
    }

    input:focus {
      border-color: #a259ff;
      box-shadow: 0 0 10px rgba(162,89,255,0.7);
    }

    button {
      padding: 12px 16px;
      border: none;
      border-radius: 10px;
      background: linear-gradient(135deg, #7d3cff, #a259ff);
      color: #fff;
      font-weight: bold;
      cursor: pointer;
      transition: 0.3s;
      box-shadow: 0 0 10px rgba(162,89,255,0.6);
    }

    button:hover {
      transform: scale(1.05);
      box-shadow: 0 0 15px rgba(162,89,255,1);
    }

    #taskCounter {
      margin-top: 15px;
      font-weight: bold;
      text-align: center;
      color: #bbb;
    }

    h2 {
      margin-top: 25px;
      font-size: 18px;
      color: #a259ff;
      text-shadow: 0 0 8px rgba(162,89,255,0.6);
    }

    ul {
      list-style: none;
      padding: 0;
      margin-top: 10px;
    }

    li {
      background: #262626;
      padding: 12px 15px;
      border-radius: 12px;
      margin-bottom: 12px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-left: 4px solid #a259ff;
      font-size: 16px;
      color: #eee;
      transition: 0.3s;
    }

    li:hover {
      background: #333;
    }

    li.completed {
      text-decoration: line-through;
      color: #888;
      border-left: 4px solid #555;
    }

    .actions {
      display: flex;
      gap: 8px;
    }

    .actionBtn {
      border: none;
      background: none;
      cursor: pointer;
      font-size: 16px;
      padding: 4px 8px;
      border-radius: 6px;
      transition: 0.3s;
    }

    .completeBtn {
      color: #00ffcc;
      text-shadow: 0 0 6px rgba(0,255,200,0.8);
    }

    .completeBtn:hover {
      background: rgba(0, 255, 200, 0.1);
    }

    .deleteBtn {
      color: #ff4d4d;
      text-shadow: 0 0 6px rgba(255,77,77,0.8);
    }

    .deleteBtn:hover {
      background: rgba(255, 77, 77, 0.1);
    }

    footer {
      text-align: center;
      margin-top: 25px;
      font-size: 13px;
      color: #888;
    }
  </style>
</head>
<body>
  <div class="todo-container">
    
    <!-- Header Section -->
    <h1>✨ My To-Do App ✨</h1>
    <p class="subtitle">Stay productive, stay organized 💪</p>

    <!-- Instructions -->
    <div class="instructions">
      <p>➡️ Type your task in the box below and click <strong>Add</strong>.</p>
      <p>✔️ Click on a task to mark it as <strong>completed</strong>.</p>
      <p>❌ Use delete button to remove unwanted tasks.</p>
    </div>

    <!-- Input Section -->
    <div class="input-section">
      <input type="text" id="taskInput" placeholder="Enter a new task...">
      <button onclick="addTask()">➕ Add</button>
    </div>

    <!-- Task Counter -->
    <p id="taskCounter">You have <span>0</span> pending tasks 📝</p>

    <!-- Task Lists -->
    <h2>📂 Today’s Tasks</h2>
    <ul id="taskList"></ul>

    <h2>✅ Completed Tasks</h2>
    <ul id="completedList"></ul>

    <!-- Footer -->
    <footer>
      <p>💡 Pro Tip: Break big goals into small steps!</p>
      <p>Made with ❤️ using HTML, CSS & JavaScript</p>
    </footer>
  </div>

  <script>
    const taskInput = document.getElementById("taskInput");
    const taskList = document.getElementById("taskList");
    const completedList = document.getElementById("completedList");
    const taskCounter = document.getElementById("taskCounter").querySelector("span");

    function updateCounter() {
      const pendingTasks = taskList.children.length;
      taskCounter.textContent = pendingTasks;
    }

    function addTask() {
      const taskText = taskInput.value.trim();
      if (taskText === "") {
        alert("Please enter a task!");
        return;
      }

      const li = document.createElement("li");
      li.textContent = taskText;

      const actions = document.createElement("div");
      actions.classList.add("actions");

      const completeBtn = document.createElement("button");
      completeBtn.textContent = "✔️";
      completeBtn.classList.add("actionBtn", "completeBtn");
      completeBtn.onclick = () => {
        li.classList.add("completed");
        completedList.appendChild(li);
        actions.remove();
        updateCounter();
      };

      const deleteBtn = document.createElement("button");
      deleteBtn.textContent = "❌";
      deleteBtn.classList.add("actionBtn", "deleteBtn");
      deleteBtn.onclick = () => {
        li.remove();
        updateCounter();
      };

      actions.appendChild(completeBtn);
      actions.appendChild(deleteBtn);
      li.appendChild(actions);
      taskList.appendChild(li);

      taskInput.value = "";
      updateCounter();
    }

    updateCounter();
  </script>
</body>
</html>
```


## OUTPUT
<img width="1476" height="901" alt="ex3 todo mwa" src="https://github.com/user-attachments/assets/097e706a-d5b3-4d1a-ba14-6ca35e1150aa" />


## RESULT
The program for creating To-do list using JavaScript is executed successfully.
