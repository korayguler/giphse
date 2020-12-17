<template>
  <div class="search-nav">
    <input
      type="text"
      v-model="searchQuery"
      @keypress.enter="searchRequested"
      class="search-input"
      placeholder="search gif."
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: '',
    };
  },
  methods: {
    searchRequested() {
      this.$emit('SearchRequested', this.searchQuery);
    },
  },
};
</script>

<style>
.search-nav {
  width: 100%;
  height: 70px;
  background: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  padding: 10px 50px;
}

.search-nav .search-input {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen,
    Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 800;
  color: #444;
  height: 100%;
  width: 100%;
  max-width: 400px;
  font-size: 40px;
  text-align: center;
  border-radius: 10px;
  outline: 0;
  border: 0;
  background: transparent;
  box-shadow: inset 0 0 8px rgba(0, 0, 0, 0.2);
}
</style>
