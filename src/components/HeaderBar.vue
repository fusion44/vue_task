<template>
  <header>
    <h1>{{ title }}</h1>
    <StyledButton
      v-show="homePage"
      @btn-click="$emit('toggle-add-task-ui')"
      :text="showAddTask ? 'Close' : 'Add Task'"
      :color="showAddTask ? 'red' : 'green'"
    />
  </header>
</template>

<script>
import StyledButton from "./StyledButton.vue";

export default {
  name: "HeaderBar",
  props: {
    title: {
      type: String,
      default: "Task Tracker",
    },
    showAddTask: Boolean,
  },
  computed: {
    homePage() {
      if (this.$route.path === "/") {
        return true;
      } else {
        return false;
      }
    },
  },
  components: {
    StyledButton,
  },
  emits: ["toggle-add-task-ui"],
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>