<template>
  <div class="app-popup" @click="hidePopup">
    <div class="app-popup__inner" @click.stop>
      <span class="app-popup__title">Информация о сотруднике</span>
      <button class="app-popup__close-btn" @click="hidePopup">&times;</button>
      <form class="app-popup__form" @submit.prevent="submitForm">
        <label class="app-popup__label">
          <span class="app-popup__label-text">Имя</span>
          <input
            class="app-popup__label-input"
            type="text"
            v-model="person.name"
            v-focus
            required
          />
        </label>
        <label class="app-popup__label">
          <span class="app-popup__label-text">Телефон</span>
          <the-mask
            class="app-popup__label-input"
            mask="+7 ### ### ## ##"
            v-model="person.phoneNumber"
            type="tel"
            masked="false"
            placeholder="+7 ___ ___ __ __"
            required
          ></the-mask>
        </label>
        <label class="app-popup__label" v-if="allPeople.length">
          <span class="app-popup__label-text">Начальник</span>
          <select class="app-popup__label-select" v-model="person.bossId">
            <option value=""></option>
            <option
              v-for="person of allPeople"
              :key="person.id"
              :value="person.id"
              >{{ person.name }}</option
            >
          </select>
        </label>
        <app-btn class="app-popup__btn" type="submit">Сохранить</app-btn>
      </form>
    </div>
  </div>
</template>

<script>
import AppBtn from '@/components/UI/AppBtn'
import { TheMask } from 'vue-the-mask'

export default {
  name: 'AppPopup',

  components: {
    AppBtn,
    TheMask
  },

  data() {
    return {
      person: {
        name: '',
        phoneNumber: '+7(',
        id: null,
        bossId: '',
        subordinates: []
      }
    }
  },

  props: {
    allPeople: {
      type: Array,
      required: true
    }
  },

  methods: {
    hidePopup() {
      this.$emit('hidePopup')
    },

    hidePopupOnEsc(e) {
      return e.code === 'Escape' ? this.hidePopup() : undefined
    },

    createPerson() {
      this.person.id = Date.now()
      this.$emit('add-person', this.person)
    },

    submitForm() {
      this.createPerson()
      this.hidePopup()
    }
  },

  directives: {
    focus: {
      inserted: function(el) {
        el.focus()
      }
    }
  },

  mounted() {
    document.addEventListener('keydown', e => {
      this.hidePopupOnEsc(e)
    })
  },

  beforeUnmount() {
    document.removeEventListener('keydown', e => {
      this.hidePopupOnEsc(e)
    })
  }
}
</script>

<style scoped lang="scss">
.app-popup {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  display: flex;
  align-items: center;
  justify-content: center;
  padding: 16px;

  background: rgba(0, 0, 0, 0.6);

  &__inner {
    position: relative;

    flex-basis: 360px;
    padding: 32px;
    display: flex;
    flex-direction: column;
    gap: 24px;

    background-color: #fff;
    border-radius: 4px;
  }

  &__title {
    font-weight: 700;
    font-size: 18px;
    color: gray;
  }

  &__close-btn {
    position: absolute;
    top: 16px;
    right: 16px;

    appearance: none;
    outline: none;
    border: none;
    background: none;
    cursor: pointer;

    width: 32px;
    height: 32px;
    display: flex;
    align-items: center;
    justify-content: center;

    background-image: linear-gradient(to right, #cc2e5d, #ff5858);
    border-radius: 4px;

    color: #fff;
    font-size: 24px;
    line-height: 0;

    transition: 0.2s ease-out;

    &:active {
      opacity: 0.7;
    }
  }

  &__form {
    display: flex;
    flex-direction: column;
    gap: 8px;
    color: gray;
  }

  &__label {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    justify-content: space-between;
    align-items: center;
  }

  &__label-input,
  &__label-select {
    width: 160px;
    padding: 8px;
    border: 1px solid grey;
    border-radius: 4px;

    &:focus {
      outline-color: darkgray;
    }
  }

  &__btn {
    margin-top: 16px;
  }
}
</style>
