<template>
  <button @click="click" :class="className" class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: ["click", "className"],
};
</script>

<style lang="scss" scoped>
.btn {
  display: inline-block;
  border: unset;
  font-size: 16px;
  font-weight: 600;
  text-transform: uppercase;
  color: #fff;
  padding: 8px 24px;
  border-radius: 12px;
  cursor: pointer;
  box-shadow: 1px 1px 10px rgba($color: #000, $alpha: 0.4);
  transition: box-shadow 0.35s ease-out;

  &:hover {
    box-shadow: 1px 1px 10px rgba($color: #000, $alpha: 0.4),
      6px 6px 12px rgba(0, 0, 0, 0.2);
  }

  & + & {
    margin-left: 16px;
  }

  &.prev {
    background-color: #72e6b1;
  }
  &.next {
    background-color: #1e68cf;
  }
  &.reset {
    background-color: #1d719a;
  }
}
</style>
