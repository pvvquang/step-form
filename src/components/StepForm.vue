<template>
  <div class="form-step">
    <progress-bar :step="formActive" />
    <div class="form-step__wrap">
      <div class="form-step__title">
        <form-title
          v-for="(item, index) in steps"
          :key="index"
          :number="item.step"
          :className="{
            active: item.step === formActive,
            success: item.validated,
          }"
          >{{ item.name }}</form-title
        >
      </div>
    </div>
    <div class="form-step__wrap">
      <div class="form-step__group">
        <custom-input type="text" id="name">Full Name</custom-input>
        <custom-input type="email" id="email">Your Email</custom-input>
      </div>
      <div class="form-step__group" v-if="steps[0].validated">
        <custom-input type="text" id="company">Your Company Name</custom-input>
        <custom-input type="text" :typeCustom="number" id="employees"
          >Number of Employees</custom-input
        >
      </div>
    </div>
    <div class="form-step__btns">
      <Button :click="handlePrev" className="prev">Previous</Button>
      <Button :click="handleNext" className="next">Next</Button>
      <Button :click="handleReset" v-if="formAction === 3" className="reset"
        >Reset</Button
      >
    </div>
  </div>
</template>

<script>
import ProgressBar from "./ProgressBar.vue";
import FormTitle from "./FormTitle.vue";
import CustomInput from "./CustomInput.vue";
import Button from "./Button.vue";

export default {
  name: "StepForm",
  data() {
    return {
      steps: [
        { step: 1, validated: false, name: "About You" },
        { step: 2, validated: false, name: "About your Company" },
        { step: 3, validated: false, name: "Finishing Up" },
      ],
      formActive: 1,
    };
  },
  components: {
    FormTitle,
    ProgressBar,
    CustomInput,
    Button,
  },
  methods: {
    handlePrev() {},
    handleNext() {},
    handleReset() {},
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.form-step {
  width: 900px;
  margin: 0 auto;

  &__wrap {
    border-radius: 12px;
    background-color: #fff;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2), 6px 12px 20px rgba(0, 0, 0, 0.1);
    margin-top: 15px;
    padding: 20px;
  }

  &__title {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  &__btns {
    margin-top: 50px;
  }
}
</style>
