<template>
  <div class="container">
    <HeaderBox @toggle-add-task="toggleAddTask" title="Task Manager" :showAddTask="showAddTask" />
    <div v-if="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    
    <TasksVue @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
  </div>
</template>

<script>

import HeaderBox from './components/Header.vue'
import TasksVue from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    HeaderBox,
    TasksVue,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },
  methods: {
    toggleAddTask() {
      console.log("toggled add task")
      this.showAddTask = !this.showAddTask
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id) {
      if(confirm('Are you sure')) {
        this.tasks = this.tasks.filter((tasks) => tasks.id !== id)
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
      task.id === id ? {...task, reminder: !task.
        reminder} : task)
    }
  },
  created() {
    this.tasks = [{
      id: 1,
      text: "Doctors appointment",
      day: "March 1st at 2:30pm",
      reminder: true,
    },{
      id: 2,
      text: "Doctors appointment 2",
      day: "March 2st at 2:30pm",
      reminder: true,
    },{
      id: 3,
      text: "Doctors appointment 3",
      day: "March 3st at 2:30pm",
      reminder: false,
    }]
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
