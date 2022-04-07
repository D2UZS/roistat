<template>
  <details>
    <summary class="table-row" :class="{ spoller: person.subordinates.length }">
      <div
        class="table-row__cell"
        :class="{ spoller__btn: person.subordinates.length }"
      >
        {{ person.name }}
      </div>
      <div class="table-row__cell">{{ person.phoneNumber }}</div>
    </summary>
    <table-row
      v-for="subordinate of person.subordinates"
      :key="subordinate.id"
      :person="subordinate"
    />
  </details>
</template>

<script>
export default {
  name: 'TableRow',
  props: {
    person: {
      type: Object,
      required: true
    }
  },
  data() {
    return {}
  }
}
</script>

<style scoped>
.table-row {
  display: grid;
  grid-template-columns: auto 200px;
}

.table-row__cell {
  padding: 8px;
  border: 1px solid black;
  box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);
  background-color: azure;
}

.table-row__cell:not(:nth-child(even)) {
  border-right: none;
}

details details {
  padding-left: 4px;
}

.spoller {
  cursor: pointer;
}

.spoller__btn::before {
  content: '+';
}

details[open] > summary > .spoller__btn::before {
  content: '-';
}
</style>
