<template>
  <div class="alphabet-list-item">
    <p class="list-divider">{{ groupName }}</p>
    <ul class="list-item">
      <li class="item" v-for="(item, index) in sortedItems" :key="index">
        {{ item.english }}
        <img class="flag" src="@/assets/flag-cook-islands.png" />
        {{ item.maori }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "AlphabetListItem",
  props: {
    groupName: {
      type: String,
      default: "",
    },
    items: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  computed: {
    sortedItems() {
      const toUpperCase = (key) => (obj) => obj[key].toUpperCase();
      const titleUpperCase = toUpperCase("english");
      const sort = (v1, v2) =>
        titleUpperCase(v1) === titleUpperCase(v2)
          ? 0
          : titleUpperCase(v1) > titleUpperCase(v2)
          ? 1
          : -1;

      return this.items.sort(sort);
    },
  },
};
</script>

<style lang="scss" scoped>
.list-divider {
  font-size: 0.8em;
  font-weight: bold;
  background: #e5e5e5;
  padding: 5px;
}

.flag {
  margin-top: 5px;
  width: 20px;
  height: 20px;
}

.item {
  font-size: 1.1em;
  padding: 10px;
  background: white;
  border-bottom: 1px solid #c3c3c3;
  box-sizing: border-box;
  font-family: "SUSE", sans-serif;

  &:last-child {
    border-color: transparent;
  }
}
</style>
