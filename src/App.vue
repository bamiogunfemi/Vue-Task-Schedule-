<template>
  <div class="container">
    <Header
      :showAddTask="showAddTask"
      @toggle-add-task="toggleAddTask"
      title="Task Tracker"
    />
    <div v-if="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import Header from "./components/Header";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask";
export default {
  name: "App",
  components: { Header, Tasks, AddTask },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    addTask(task) {
      console.log(task, "e", this.tasks);
      this.tasks = [...this.tasks, task];
    },
    deleteTask(id) {
      if (confirm("Are you sure you want to delete this task?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
  },
  created() {
    this.tasks = [
      {
        id: "1",
        text: "Doctors Appointment",
        day: "March 5th at 2:30pm",
        reminder: true,
      },
      {
        id: "2",
        text: "Meeting with boss",
        day: "March 6th at 1:30pm",
        reminder: true,
      },
      {
        id: "3",
        text: "Food shopping",
        day: "March 7th at 2:00pm",
        reminder: false,
      },
    ];
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
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
