<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')"  :class="{ active: current === 'all'}"> View All</button>
    <button @click="updateFilter('completed')" :class="{ active: current === 'completed'}"> View Completed</button>
    <button @click="updateFilter('ongoing')" :class="{ active: current === 'ongoing'}"> View Ongoing</button>
  </nav>
</template>

<script>
export default {
  props: ['current'],
  methods: {
    updateFilter(filterBy) {
      this.$emit('filterChange', filterBy)
    }
  }
}
</script>

<style>
  .filter-nav button {
    background: none;
    border:none;
    color:#bbb;
    outline:none;
    font-size:12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
    padding: 10px;
    border:1px solid transparent;
    border-radius:4px;
  }
  .filter-nav button:hover {
    background: #fff;
    border:1px solid #00ce49;
    color:#00ce49;
  }
  button.active{
    background: #fff;
    border:1px solid #00ce49;
    color:#00ce49;
  }
</style>