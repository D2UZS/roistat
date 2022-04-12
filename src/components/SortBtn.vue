<template>
  <div class="sort-btn" @click="toggleSort">
    <slot></slot>
    <svg
      class="sort-btn__icon"
      width="17"
      height="16"
      viewBox="0 0 17 16"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path
        class="sort-btn__icon-arrow"
        :class="{
          'sort-btn__icon-arrow--active': this.sortParam === 'reversAlphabet'
        }"
        d="M5.63261 5.69134C5.69895 5.87818 5.85522 6 6.02856 6H11.1714C11.3447 6 11.501 5.87818 11.5673 5.69134C11.6337 5.5045 11.597 5.28944 11.4744 5.14645L8.90302 2.14644C8.73566 1.95118 8.4643 1.95118 8.29693 2.14644L5.72551 5.14645C5.60294 5.28944 5.56628 5.5045 5.63261 5.69134Z"
      />
      <path
        class="sort-btn__icon-arrow"
        :class="{
          'sort-btn__icon-arrow--active': this.sortParam === 'alphabet'
        }"
        d="M5.63261 10.3087C5.69895 10.1218 5.85522 10 6.02856 10H11.1714C11.3447 10 11.501 10.1218 11.5673 10.3087C11.6337 10.4955 11.597 10.7106 11.4744 10.8536L8.90302 13.8536C8.73566 14.0488 8.4643 14.0488 8.29693 13.8536L5.72551 10.8536C5.60294 10.7106 5.56628 10.4955 5.63261 10.3087Z"
      />
    </svg>
  </div>
</template>

<script>
export default {
  name: 'SortBtn',

  data() {
    return {
      sortParam: ''
    }
  },

  methods: {
    toggleSort() {
      this.sortParam === '' || this.sortParam === 'reversAlphabet'
        ? (this.sortParam = 'alphabet')
        : (this.sortParam = 'reversAlphabet')

      this.$emit('changeSortParam', this.sortParam)
    }
  }
}
</script>

<style scoped lang="scss">
.sort-btn {
  display: flex;
  align-items: center;
  gap: 8px;
  justify-content: space-between;
  cursor: pointer;
  user-select: none;

  &__icon {
    fill: #a0a0a0;

    &-arrow {
      &--active {
        fill: #d0021b;
      }
    }
  }
}
</style>
