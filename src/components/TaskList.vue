<template>
  <div :key="t.id" v-for="t in tasks">
    <TaskItem
      @toggle-reminder="$emit('toggle-reminder', t.id)"
      @delete-task="$emit('delete-task', t.id)"
      :task="t"
    />
  </div>
</template>

<script>
import TaskItem from "./TaskItem.vue";

export default {
  name: "TaskList",
  props: {
    tasks: Array,
  },
  components: { TaskItem },
  emits: ["delete-task", "toggle-reminder"],
};
</script>

<style>
</style>