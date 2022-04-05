<template>
  <div class="app-table">
    <div class="app-table__cell">Имя</div>
    <div class="app-table__cell">Телефон</div>
  </div>
</template>

<script>
export default {
  name: 'AppTable',
  data() {
    return {}
  }
}
</script>

<style scoped>
.app-table {
  display: grid;
  grid-template-columns: 40% 60%;
}
.app-table__cell {
  padding: 8px;
  border: 1px solid black;
}

.app-table__cell:nth-child(even) {
  border-left: none;
}
</style>
