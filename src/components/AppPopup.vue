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
          <input
            class="app-popup__label-input"
            type="tel"
            v-model="person.phoneNumber"
            placeholder="+7(___)___-__-__"
          />
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

export default {
  name: 'AppPopup',

  components: {
    AppBtn
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

<style scoped>
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
}

.app-popup__inner {
  position: relative;

  flex-basis: 360px;
  padding: 32px;
  display: flex;
  flex-direction: column;
  gap: 24px;

  background-color: #fff;
  border-radius: 4px;
}

.app-popup__title {
  font-weight: 700;
  font-size: 18px;
  color: gray;
}

.app-popup__close-btn {
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
}

.app-popup__close-btn:active {
  opacity: 0.7;
}

.app-popup__form {
  display: flex;
  flex-direction: column;
  gap: 8px;
  color: gray;
}

.app-popup__label {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  justify-content: space-between;
  align-items: center;
}

.app-popup__label-input,
.app-popup__label-select {
  width: 160px;
  /* height: 38px; */
  padding: 8px;
  border: 1px solid grey;
  border-radius: 4px;
}

.app-popup__label-input:focus,
.app-popup__label-select:focus {
  outline-color: darkgray;
}

.app-popup__btn {
  margin-top: 16px;
}
</style>
