<template>
  <div class="option__item" @click="$emit('selectClick', item)">
    {{ item }}
    <slot></slot>
  </div>
</template>

<script>
export default {
  props: ["item"],
};
</script>

<style lang="scss" scoped>
.option__item {
  padding: 8px 16px;
  background-color: #fff;
  transition: background-color 0.2s ease-in;

  &:hover {
    background-color: #ccc;
  }
}
</style>
