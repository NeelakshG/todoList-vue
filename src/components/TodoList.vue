<script setup>
import { ref } from "vue";

//setting up the state
const newTask = ref("");
const tasks = ref([]);

//adding a task if and only if the task user writes down actually exists
const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";

    console.log("Enter key pressed. Task to add:", newTask.value);
  }
};

//removing a task
const removeTask = (index) => {
  tasks.value.splice(index, 1); //splice(index,number) --> index refers to the position in the array, number refers to how many you wanna delete
};
</script>

<template>
  <!-- we have a div that sets up all of the ui -->
  <div class="todo-app">
    <!-- one of the divs is used for the input -->
    <div class="task-input">
      <!-- v-model binds the newTask input into the newTask variable -->
      <!-- keyup.enter just means anytime the keyword enter is clicked, the function addTask is called -->
      <input
        v-model="newTask"
        @keyup.enter="addTask"
        placeholder="Add a new task"
      />
      <!-- when clicked, we call the addTask method -->
      <button @click="addTask">Add To Do</button>
    </div>

    <ul class="task-list">
      <!-- prints out every task in the array tasks -->
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        {{ task }}
        <!-- for each button make sure there is a remove option so that user is able to remove -->
        <button @click="removeTask(index)" class="remove-button">Remove</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.todo-app {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.app-title {
  font-size: 40p;
  margin-bottom: 20px;
  text-align: center;
  color: #333;
}

.task-input {
  display: flex;
  gap: 10px;
}

input {
  flex: 1;
  padding: 8px;
  font-size: 14px;
}

button {
  padding: 8px 12px;
  font-size: 14px;
  background-color: #4caf50;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}

.task-list {
  list-style: none;
  padding: 0;
}

.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  margin: 8px 0;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.remove-button {
  padding: 6px 10px;
  font-size: 12px;
  background-color: #e74c3c;
  color: #fff;
  border: none;
  border-radius: 3px;
  cursor: pointer;
}

.remove-button:hover {
  background-color: #c0392b;
}
</style>
