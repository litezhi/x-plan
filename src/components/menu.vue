<template>
  <ul class="x-menu x-glass">
    <li
      v-for="item in dataSource"
      :key="item.key"
      @click="handleClick(item)"
      :class="[
        'x-menu-item',
        item.key === selected ? 'x-menu-item--selected' : '',
      ]"
    >
      {{ item.title }}
    </li>
    <li class="x-menu-suffix">
      <slot name="suffix"></slot>
    </li>
  </ul>
</template>

<script lang="ts">
import { reactive, ref } from "vue";

export default {
  name: "Menu",
  props: {
    dataSource: {
      default: [],
      type: Array,
      required: true,
    },
  },
  setup(props, context) {
    const selected = ref(null);

    const handleClick = (item, event) => {
      selected.value = item.key;
      context.emit("select", item);
    };

    return { handleClick, selected };
  },
};
</script>

<style>
.x-menu {
  display: flex;
  height: 60px;
  line-height: 60px;
  list-style: none;
  margin: 0;
  padding: 0 16px;
}
.x-menu .x-menu-item {
  color: #eee;
  cursor: pointer;
  padding: 0 8px;
  transition: all 0.2s ease-in-out;
}
.x-menu .x-menu-item:hover {
  background: rgba(255, 255, 255, 0.2);
  color: #fff;
}
.x-menu .x-menu-item.x-menu-item--selected {
  background-color: rgba(255, 255, 255, 0.2);
}
.x-menu .x-menu-suffix {
  margin-left: auto;
}
.x-menu .x-menu-suffix .x-button {
  margin-right: 8px;
}
</style>
