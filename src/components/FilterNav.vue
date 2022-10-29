<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')" :class="{ active: current === 'all' }">
      View All
    </button>
    <button
      @click="updateFilter('completed')"
      :class="{ active: current === 'completed' }"
    >
      View Completed
    </button>
    <button
      @click="updateFilter('ongoing')"
      :class="{ active: current === 'ongoing' }"
    >
      View Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: ["current"],
  methods: {
    updateFilter(by) {
      this.$emit("filterChange", by);
    },
  },
};
</script>

<style>
.filter-nav {
  text-align: center;
}
.filter-nav button {
  background: none;
  border: none;
  outline: none;
  color: #eee;
  font-size: 1em;
  text-transform: uppercase;
  margin-right: 1em;
  letter-spacing: 0.1em;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.25s linear;
}
.filter-nav button.active {
  color: #222;
}
.filter-nav button:hover {
  color: #444;
}
</style>
