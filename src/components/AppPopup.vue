<template>
  <div class="app-popup">
    <form class="app-popup__form">
      <label class="app-popup__label">
        <span class="app-popup__label-text">Имя</span>
        <input class="app-popup__label-input" type="text" />
      </label>
      <label class="app-popup__label">
        <span class="app-popup__label-text">Телефон</span>
        <input class="app-popup__label-input" type="tel" />
      </label>
      <label class="app-popup__label">
        <span class="app-popup__label-text">Начальник</span>
        <select class="app-popup__label-select">
          <option value="1">1</option>
          <option value="2">2</option>
          <option value="3">3</option>
        </select>
      </label>
      <app-btn class="app-popup__btn" type="submit">Сохранить</app-btn>
    </form>
  </div>
</template>

<script>
import AppBtn from '@/components/UI/AppBtn'

export default {
  name: 'AppPopup',
  components: {
    AppBtn
  },
  data() {
    return {}
  }
}
</script>

<style scoped></style>
