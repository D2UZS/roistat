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
  }
}
</script>

<style scoped>
.table-row {
  display: grid;
  grid-template-columns: auto 200px;
  box-shadow: 3px 3px rgba(0, 0, 0, 0.4);
}

.table-row__cell {
  padding: 8px;
  border: 1px solid grey;
  background-color: #fff;
}

details details {
  padding-left: 8px;
}

.spoller {
  cursor: pointer;
}

.spoller__btn::before {
  content: '+';
}

details[open] > .table-row > .spoller__btn::before {
  content: '-';
}
</style>
