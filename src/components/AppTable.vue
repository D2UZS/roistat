<template>
  <div class="app-table">
    <div class="app-table__header table-header">
      <sort-btn class="table-header__cell" @changeSortParam="sortParam = $event"
        >Имя</sort-btn
      >
      <div class="table-header__cell">Телефон</div>
    </div>
    <table-row
      v-for="person of sortedPersons"
      :key="person.id"
      :person="person"
    />
  </div>
</template>

<script>
import TableRow from '@/components/TableRow'
import SortBtn from '@/components/SortBtn'

export default {
  name: 'AppTable',
  components: {
    TableRow,
    SortBtn
  },

  props: {
    persons: {
      type: Array,
      required: true
    }
  },

  data() {
    return {
      sortParam: ''
    }
  },

  methods: {
    sortAlphabet(d1, d2) {
      return d1.name.toLowerCase() > d2.name.toLowerCase() ? 1 : -1
    },

    sortReversAlphabet(d1, d2) {
      return d1.name.toLowerCase() < d2.name.toLowerCase() ? 1 : -1
    },

    sortPersonsSubordinates(obj, sortFunction) {
      for (const iterator of obj) {
        if ('subordinates' in iterator) {
          this.sortPersonsSubordinates(iterator.subordinates, sortFunction)
          iterator.subordinates = [...iterator.subordinates].sort(sortFunction)
        }
      }
    },

    sortPersons(sortFunction) {
      this.sortPersonsSubordinates(this.persons, sortFunction)
      return [...this.persons].sort(sortFunction)
    }
  },

  computed: {
    sortedPersons() {
      switch (this.sortParam) {
        case 'alphabet':
          return this.sortPersons(this.sortAlphabet)
        case 'reversAlphabet':
          return this.sortPersons(this.sortReversAlphabet)
        default:
          return this.persons
      }
    }
  }
}
</script>

<style scoped>
.app-table__header {
  display: grid;
  grid-template-columns: auto 200px;
}

.table-header__cell {
  padding: 12px 8px;
  border: 1px solid grey;
  box-shadow: 3px 3px rgba(0, 0, 0, 0.4);
  background-color: #fff;
  font-weight: 700;
}
</style>
