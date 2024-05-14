<template>
  <div class="app">
    <h1 style="color: #4caf50;">To-Do List</h1>
    <div class="info-container">
      <div class="info-item">
        <label for="name">Name:</label>
        <input id="name" v-model="name" placeholder="Your name">
      </div>
      <div class="info-item">
        <label for="date">Date:</label>
        <input id="date" type="date" v-model="date">
      </div>
      <div class="info-item">
        <label for="email">Email:</label>
        <input id="email" type="email" v-model="email" placeholder="Your email">
      </div>
    </div>
    <div class="input-container">
      <input v-model="newTask" @keyup.enter="addTask" placeholder="Add New Task" style="background-color: #f5f5f5; color: #333;">
      <button @click="addTask" class="add-button">Add</button>
    </div>
    <div v-if="tasks.length === 0" class="empty-message" style="color: #f44336;">No tasks yet.</div>
    <transition-group name="fade">
      <div v-for="(task, index) in tasks" :key="index" class="task-item" style="background-color: #fff; box-shadow: 0 0 10px rgba(0, 0, 0, 0.1); color: #333;">
        <input type="checkbox" v-model="task.completed" class="task-checkbox" style="margin-right: 15px;">
        <span :class="{ completed: task.completed }">{{ task.text }}</span>
        <button @click="deleteTask(index)" class="delete-button" style="background-color: #f44336;">X</button>
      </div>
    </transition-group>
    <div class="buttons">
      <button @click="clearCompleted" class="clear-button" style="background-color: #f44336;">Clear Completed</button>
      <button @click="clearAll" class="clear-button" style="background-color: #ff9800;">Clear All</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      name: '',
      date: '',
      email: '',
      tasks: []
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ text: this.newTask, completed: false });
        this.newTask = '';
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    clearCompleted() {
      this.tasks = this.tasks.filter(task => !task.completed);
    },
    clearAll() {
      this.tasks = [];
    }
  }
};
</script>

<style scoped>
.app {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f5f5f5;
  border-radius: 10px;
}

h1 {
  text-align: center;
}

.info-container {
  background-color: #fff;
  padding: 20px;
  border-radius: 10px;
  margin-bottom: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.info-item {
  margin-bottom: 10px;
}

input {
  width: calc(100% - 70px);
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ccc;
}

.add-button {
  width: 70px;
  padding: 10px;
  border: none;
  border-radius: 5px;
  background-color: #4caf50;
  color: #fff;
  cursor: pointer;
  transition: background-color 0.3s;
}

.add-button:hover {
  background-color: #45a049;
}

.empty-message {
  text-align: center;
  margin-bottom: 20px;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0;
}

.task-item {
  display: flex;
  align-items: center;
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.task-checkbox {
  margin-right: 15px;
}

.completed {
  text-decoration: line-through;
  color: #999;
}

.delete-button {
  margin-left: auto;
  background-color: #f44336;
  color: #fff;
  border: none;
  border-radius: 50%;
  padding: 8px 12px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.delete-button:hover {
  background-color: #c62828;
}

.buttons {
  display: flex;
  justify-content: space-between;
}

.clear-button {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.clear-button:hover {
  filter: brightness(90%);
}
</style>
