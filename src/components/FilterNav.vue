<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')" :class="{ active: this.currentFilter === 'all' }">
      All
    </button>
    <button @click="updateFilter('completed')" :class="{ active: this.currentFilter === 'completed' }">
      Completed
    </button>
    <button @click="updateFilter('ongoing')" :class="{ active: this.currentFilter === 'ongoing' }">
      Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: [ 'currentFilter' ],
  data() {
    return {
    }
  },
  methods: {
    updateFilter(args) {
      this.$emit('filterChange', args)
    },
  },
  mounted() {
  }
}
</script>

<style>
.filter-nav button {
  background-color: transparent;
  border: none;
  color: #bbb;
  outline: none;
  font-size: 1rem;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
  transition: border-bottom 0.5s ease;
  border-bottom: 4px solid transparent;
}
.filter-nav .active {
  border-bottom: 4px solid #00ce89;
}
</style>
