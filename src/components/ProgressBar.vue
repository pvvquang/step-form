<template>
  <div class="progress-border">
    <div class="progress-content" :style="{ width: width + '%' }"></div>
  </div>
</template>

<script>
export default {
  props: ["step","max"],
  computed: {
    width() {
      return Math.ceil((+this.step / this.max) * 100);
    },
  },
};
</script>

<style lang="scss" scoped>
.progress {
  &-border {
    width: 100%;
    height: 18px;
    background-color: #fff;
    border-radius: 12px;
    overflow: hidden;
  }

  &-content {
    height: 100%;
    background-color: #437fe8;
    border-radius: 12px;
    transition: width 0.5s ease;
  }
}
</style>
