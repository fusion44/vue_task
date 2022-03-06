<template>
  <button
    @click="$emit('btn-click')"
    :style="{ background: color }"
    class="btn"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "StyledButton",
  props: { text: String, color: String },
  emits: ["btn-click"],
};
</script>

<style>
</style>