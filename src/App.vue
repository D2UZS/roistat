<template>
  <div class="app">
    <div class="app__container">
      <button class="app__btn" @click="showPopup">Добавить сотрудника</button>
      <app-table class="app__table" :persons="persons" />
      <app-popup
        class="app__popup"
        v-if="popupIsVisible"
        @hidePopup="hidePopup"
        @add-person="addPerson"
        :allPeople="allPeople"
      />
    </div>
  </div>
</template>

<script>
import AppTable from '@/components/AppTable'
import AppPopup from '@/components/AppPopup'

export default {
  name: 'App',

  components: {
    AppTable,
    AppPopup
  },

  data() {
    return {
      popupIsVisible: false,

      persons: [
        {
          name: 'Марина',
          phoneNumber: '+7 941 123 21 42',
          id: '1',
          bossId: null,
          subordinates: [
            {
              name: 'Лена',
              phoneNumber: '+7 941 123 21 42',
              id: '3',
              bossId: null,
              subordinates: []
            },
            {
              name: 'Катя',
              phoneNumber: '+7 941 123 21 42',
              id: '7',
              bossId: null,
              subordinates: []
            }
          ]
        },
        {
          name: 'Петр',
          phoneNumber: '+7 941 123 21 42',
          id: '2',
          bossId: null,
          subordinates: []
        }
      ],

      allPeople: []
    }
  },

  methods: {
    showPopup() {
      this.popupIsVisible = true
    },

    hidePopup() {
      this.popupIsVisible = false
    },

    addPerson(person) {
      if (person.bossId) {
        const boss = this.findBoss(this.persons, person.bossId)

        boss.subordinates.push(person)
      } else {
        this.persons.push(person)
      }
      this.allPeople.push(person)
      localStorage.setItem('persons', JSON.stringify(this.persons))
    },

    findBoss(object, id) {
      for (const iterator of object) {
        const result = this.findBossRecursively(iterator, id)
        if (result) {
          return result
        }
      }
    },

    findBossRecursively(obj, id) {
      if (obj.id === id) {
        return obj
      } else if (obj.subordinates.length) {
        for (const i of obj.subordinates) {
          const result = this.findBossRecursively(i, id)
          if (result) {
            return result
          }
        }
      }
    },

    getAllPeople(array) {
      for (const obj of array) {
        if ('subordinates' in obj) {
          this.allPeople.push(obj)
          this.getAllPeople(obj.subordinates)
        } else {
          this.allPeople.push(obj)
        }
      }
    }
  },

  mounted() {
    const localPersons = localStorage.getItem('persons')
    if (localPersons) {
      this.persons = JSON.parse(localPersons)
    }
    this.getAllPeople(this.persons)
  }
}
</script>

<style>
*,
*::before,
*::after {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: 'montserrat', sans-serif;
  background-color: rgba(0, 0, 0, 0.1);
}

.app {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
}

.app__container {
  width: 100%;
  max-width: 400px;
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.app__btn {
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

  box-shadow: 3px 3px rgba(0, 0, 0, 0.4);
  transition: 0.2s ease-out;
}

.app__btn:hover {
  box-shadow: 6px 6px rgba(0, 0, 0, 0.6);
}
</style>
