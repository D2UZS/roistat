<template>
  <button class="app-btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'AppBtn'
}
</script>

<style scoped>
.app-btn {
  appearance: none;
  outline: none;
  border: none;
  background: none;
  cursor: pointer;

  display: inline-block;
  padding: 8px 16px;
  background-image: linear-gradient(to right, #cc2e5d, #ff5858);
  border-radius: 4px;

  color: #fff;
  font-size: 16px;
  font-weight: 500;

  transition: 0.2s ease-out;
}

.app-btn:active {
  opacity: 0.7;
}
</style>
