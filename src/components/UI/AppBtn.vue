<template>
  <button class="app-btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'AppBtn',
  data() {
    return {}
  }
}
</script>

<style scoped>
.app-btn {
  max-width: max-content;
  padding: 4px 8px;
  border-radius: 8px;
}
</style>
