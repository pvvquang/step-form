<template>
  <div class="title" :class="className">
    <span class="number">{{ number }}</span>
    <span class="text"><slot></slot></span>
  </div>
</template>

<script>
export default {
  props: ["number", "className"],
};
</script>

<style lang="scss" scoped>
.title {
  padding: 8px 20px;
  border-radius: 12px;
  background-color: #f3f3f3;

  &.active {
    border: 2px solid #9fbcd7;
  }

  &.success {
    border: 2px solid #32683c;
  }
}

.number {
  display: inline-block;
  font-size: 16px;
  width: 24px;
  height: 24px;
  line-height: 24px;
  border-radius: 50%;
  color: #f7f7f7;
  background-color: #969899;
  margin-right: 8px;
}

.text {
  color: #8f9294;
  font-size: 14px;
  font-weight: 500;
}
</style>
