<template>
  <AddTask v-if="showAddTask" @add-task="onAddTask" />
  <TaskList
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
const api = "http://localhost:5000";

import AddTask from "../components/AddTask";
import TaskList from "../components/TaskList";

export default {
  name: "HomeView",
  components: {
    AddTask,
    TaskList,
  },
  props: ["showAddTask"],
  data() {
    return { tasks: [] };
  },
  methods: {
    async onAddTask(task) {
      const res = await fetch(`${api}/tasks`, {
        method: "POST",
        headers: {
          "content-type": "application/json",
        },
        body: JSON.stringify(task),
      });
      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },
    async deleteTask(id) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`${api}/tasks/${id}`, {
          method: "DELETE",
        });

        if (res.status === 200) {
          this.tasks = this.tasks.filter((task) => task.id !== id);
        } else {
          alert(`Error deleting task ${id} ${res.status}`);
        }
      }
    },
    async toggleReminder(id) {
      var toggleTask = this.tasks.find((task) => task.id === id);
      var updatedTask = {
        ...toggleTask,
        reminder: !toggleTask.reminder,
      };
      const res = await fetch(`${api}/tasks/${id}`, {
        method: "PUT",
        headers: {
          "content-type": "application/json",
        },
        body: JSON.stringify(updatedTask),
      });
      const data = await res.json();

      console.log(data);
      this.tasks = this.tasks.map((task) =>
        task.id === id
          ? {
              ...task,
              reminder: data.reminder,
            }
          : task
      );
    },
    async fetchTask(id) {
      const res = await fetch(`${api}/tasks/${id}`);
      const data = await res.json();
      return data;
    },
    async fetchTasks() {
      const res = await fetch(`${api}/tasks`);
      const data = await res.json();
      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>

<style>
</style>