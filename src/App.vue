<template>
  <div class="app">
    <div class="app__container">
      <button class="app__btn" @click="showPopup">Добавить</button>
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
import AppBtn from '@/components/UI/AppBtn'

export default {
  name: 'App',

  components: {
    AppTable,
    AppBtn,
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
          chiefId: null,
          subordinates: [
            {
              name: 'Лена',
              phoneNumber: '+7 941 123 21 42',
              id: '3',
              chiefId: null,
              subordinates: []
            },
            {
              name: 'Катя',
              phoneNumber: '+7 941 123 21 42',
              id: '7',
              chiefId: null,
              subordinates: []
            }
          ]
        },
        {
          name: 'Петр',
          phoneNumber: '+7 941 123 21 42',
          id: '2',
          chiefId: null,
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
      if (person.chiefId) {
        const chiefPerson = this.findPerson(this.persons, person.chiefId)

        chiefPerson.subordinates.push(person)
      } else {
        this.persons.push(person)
      }
      this.allPeople.push(person)
      localStorage.setItem('persons', JSON.stringify(this.persons))
    },

    findPerson(object, id) {
      for (const iterator of object) {
        const result = this.foo(iterator, id)
        if (result) {
          return result
        }
      }
    },

    foo(obj, id) {
      if (obj.id === id) {
        return obj
      } else if (obj.subordinates.length) {
        for (const i of obj.subordinates) {
          const result = this.foo(i, id)
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

  max-width: max-content;
  padding: 4px 8px;
  border-radius: 8px;
}
</style>
