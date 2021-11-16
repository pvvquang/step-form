<template>
  <div class="select">
    <p class="select__label"><slot></slot></p>
    <div class="select__wrap">
      <span class="select__title" @click="showOption = !showOption">{{
        !selected ? "-- Choose anwser --" : selected
      }}</span>
      <p class="select__error"></p>
      <transition name="fade">
        <div class="select__options" v-if="showOption">
          <slot name="option"></slot>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showOption: false,
      errorMessage: "",
    };
  },
  props: ["selected"],
  watch: {
    selected() {
      this.showOption = !this.showOption;
    },
  },
};
</script>

<style lang="scss" scoped>
.select {
  text-align: left;

  &__label {
    font-size: 16px;
    color: #000;
    padding-bottom: 10px;
  }

  &__wrap {
    border: 1px solid #ccc;
    border-radius: 6px;
    position: relative;
    cursor: pointer;

    &::after {
      content: "";
      display: block;
      border: 4px solid transparent;
      border-color: #000 transparent transparent transparent;
      position: absolute;
      top: calc(50% + 3px);
      right: 22px;
      transform: translateY(-50%);
    }
  }

  &__title {
    display: block;
    width: 100%;
    height: 100%;
    padding: 10px 12px;
  }

  &__options {
    position: absolute;
    top: calc(100% + 1px);
    background-color: #fff;
    width: 100%;
    padding: 12px 0;
    box-shadow: 0 4px 8px rgba($color: #000000, $alpha: 0.2);
    border-radius: 12px;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.8s ease;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
