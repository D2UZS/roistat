<template>
  <div class="app">
    <div class="app__container">
      <app-btn class="app__btn">Добавить</app-btn>
      <app-table class="app__table" />
      <app-popup class="app__popup" />
    </div>
  </div>
</template>

<script>
import AppTable from '@/components/AppTable'
import AppPopup from '@/components/AppPopup'
import AppBtn from '@/components/UI/AppBtn'

export default {
  name: 'App',
  components: {
    AppTable,
    AppBtn,
    AppPopup
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}
.app {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;

  font-family: 'Avenir', Helvetica, Arial, sans-serif;
}

.app__container {
  width: 100%;
  max-width: 400px;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.app__btn {
  align-self: flex-end;
}
</style>
