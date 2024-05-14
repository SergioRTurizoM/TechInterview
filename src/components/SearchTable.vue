<template>
  <form>
    <div>
      <input
        type="text"
        placeholder="Search by term..."
        class="search-input"
        v-model="searchText"
      />
    </div>
  </form>
</template>

<script>
export default {
  name: "SearchTable",
  data() {
    return {
      searchText: "",
    };
  },
  watch: {
    searchText(newValue) {
      this.$emit("search", newValue);
    },
  },
};
</script>

<style>
.search-input {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 8px;
}
</style>
