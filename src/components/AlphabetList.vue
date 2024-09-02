<template>
  <div class="alphabet-list">
    <ul class="list-nav">
      <li
        class="nav-item"
        v-for="(shortcut, index) in shortcuts"
        :key="index"
        @click="moveTo(`#move_${shortcut}`)"
      >
        {{ shortcut }}
      </li>
    </ul>
    <div class="list-container" ref="list">
      <div class="list-wrapper">
        <AlphabetListItem
          v-for="(value, key, index) in groups"
          :ref="`#move_${key}`"
          :key="index"
          :groupName="key"
          :items="value"
        />
      </div>
    </div>
  </div>
</template>

<script>
import AlphabetListItem from "./AlphabetListItem";

export default {
  name: "AlphabetList",
  components: {
    AlphabetListItem,
  },
  props: {
    list: {
      type: Array,
      default() {
        return [];
      },
    },
  },
  data() {
    return {
      shortcuts: [],
      groups: {},
    };
  },
  methods: {
    groupByList(list = this.list, key = "") {
      const reducer = (result, value) => {
        const hash = (value[key] || "").charAt(0).toUpperCase();

        if (result.hasOwnProperty(hash)) {
          result[hash].push(value);
        } else {
          result[hash] = [value];
        }

        return result;
      };

      return list.reduce(reducer, {});
    },
    calcScrollTopPosition(rootElm, targetElm) {
      const { scrollTop } = rootElm;
      const {
        top: rootTop,
        left: rootLeft,
        width: rootWidth,
        height: rootHeight,
      } = rootElm.getBoundingClientRect();
      const { top, left, width, height } = targetElm.getBoundingClientRect();

      return top + scrollTop - rootTop;
    },
    moveTo(target) {
      const { list } = this.$refs;
      const [refTarget] = this.$refs[target];
      const scrollTop = this.calcScrollTopPosition(list, refTarget.$el);

      list.scrollTo(0, scrollTop);
    },
  },
  created() {
    this.groups = this.groupByList(undefined, "english");
    this.shortcuts = Object.keys(this.groups);
  },
};
</script>

<style lang="scss" scoped>
.alphabet-list {
  position: relative;
  width: 100%;
  height: 100%;
  font-family: "SUSE", sans-serif;
}

.list-container {
  width: calc(100% - 60px);
  height: 100%;
  overflow-y: scroll;
}

.list-nav {
  position: absolute;
  top: 0;
  right: 20px;
  width: 20px;
  height: 100%;
  text-align: center;

  .nav-item {
    cursor: pointer;
    font-weight: 800;
    padding: 4px;
    margin: 2.5px;
    width: 15px;
    height: 15px;

    background-color: #004eaa;
    color: white;
    border-radius: 50%;

    font-family: "SUSE", sans-serif;

    a {
      color: inherit;
      text-decoration: none;
    }
  }
}
</style>
