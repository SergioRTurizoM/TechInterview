<template>
  <div>
    <router-link
      v-for="(item, index) in items"
      :key="index"
      :to="item.path"
      class="nav-link"
      active-class="active"
    >
      {{ item.title }}
    </router-link>
  </div>
</template>

<script>
export default {
  name: "NavBarMenu",
  props: {
    items: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.nav-link {
  color: inherit;
  text-decoration: none;
  padding: 8px 16px;
}

.active {
  font-weight: bold;
}
</style>
