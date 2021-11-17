<template>
  <div class="form-step">
    <progress-bar :step="formActive" :max="steps.length"/>
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
      <div class="form-step__group" v-if="formActive === 1">
        <custom-input
          type="text"
          id="name"
          :value="user.name"
          @input="handleInputChange"
          :validFeild="validFeild"
          >Full Name</custom-input
        >
        <custom-input
          type="email"
          id="email"
          :value="user.email"
          @input="handleInputChange"
          :validFeild="validFeild"
          >Your Email</custom-input
        >
      </div>
      <div class="form-step__group" v-if="formActive === 2">
        <custom-input
          type="text"
          id="company"
          :value="user.company"
          @input="handleInputChange"
          :validFeild="validFeild"
          >Your Company Name</custom-input
        >
        <custom-input
          type="text"
          typeCustom="number"
          id="employees"
          :value="user.employees"
          @input="handleInputChange"
          :validFeild="validFeild"
          >Number of Employees</custom-input
        >
      </div>
      <div class="form-step__group" v-if="formActive === 3">
        <Select :selected="user.selected" :validFeild="validFeild">
          From Where did you hear about us
          <Option
            slot="option"
            v-for="(item, index) in listSelect"
            :key="index"
            :item="item"
            @selectClick="handleSelected"
          ></Option>
        </Select>
        <div class="check-term">
          <input type="checkbox" id="check-term" @input="handleCheckTerm" />
          <label for="check-term">I accept terms & conditions</label>
          <p class="check-term__error">{{ checkTermMessage }}</p>
        </div>
      </div>
    </div>
    <div class="form-step__btns">
      <Button
        :click="handlePrev"
        className="prev"
        v-show="formActive !== steps.length"
        >Previous</Button
      >
      <Button
        :click="handleNext"
        className="next"
        v-show="formActive !== steps.length"
        >Next</Button
      >
      <Button
        :click="handleReset"
        v-if="formActive === steps.length"
        className="reset"
        >Reset</Button
      >
      <Button
        :click="handleSubmit"
        v-if="formActive === steps.length"
        className="prev"
        >Send</Button
      >
    </div>
  </div>
</template>

<script>
import ProgressBar from "./ProgressBar.vue";
import FormTitle from "./FormTitle.vue";
import CustomInput from "./CustomInput.vue";
import Button from "./Button.vue";
import Select from "./Select.vue";
import Option from "./Option.vue";

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
      errorMessage: null,
      validFeild: null,
      user: {
        name: "",
        email: "",
        company: "",
        employees: "",
        selected: "",
        acceptTerm: false,
      },
      listSelect: ["Friend", "Facebook", "Website"],
      checkTermMessage: "",
    };
  },
  components: {
    FormTitle,
    ProgressBar,
    CustomInput,
    Button,
    Select,
    Option,
  },
  methods: {
    handlePrev() {
      if (this.formActive > 1) {
        this.steps[this.formActive - 1].validated = false;
        this.formActive = this.formActive - 1;
      }
    },

    handleNext() {
      if (this.formActive >= this.steps.length) {
        return;
      }

      switch (this.formActive) {
        case 1:
          if (this.user.name && this.user.email) {
            if (!this.errorMessage) {
              this.steps[this.formActive - 1].validated = true;
              this.formActive = this.formActive + 1;
              this.validFeild = true;
            }
          } else {
            this.validFeild = false;
          }
          break;
        case 2:
          if (this.user.company && this.user.employees) {
            if (!this.errorMessage) {
              this.steps[this.formActive - 1].validated = true;
              this.formActive = this.formActive + 1;
              this.validFeild = true;
            }
          } else {
            this.validFeild = false;
          }
          break;
      }
    },

    handleReset() {
      this.user.acceptTerm = false;
      this.user.name =
        this.user.email =
        this.user.company =
        this.user.employees =
        this.user.selected =
          "";
      this.steps.forEach((step) => (step.validated = false));
      this.formActive = 1;
      this.selected = "";
      this.validFeild = null;
    },

    handleSubmit() {
      if (!this.user.acceptTerm) {
        this.checkTermMessage = "The field is required!";
        if (!this.user.selected) {
          this.validFeild = false;
        }
      } else {
        if (!this.user.selected) {
          this.validFeild = false;
        } else {
          console.log({ userData: this.user });
        }
      }
    },

    handleInputChange(event) {
      switch (event.name) {
        case "name":
          this.user.name = event.value;
          this.errorMessage = event.errorMessage;
          break;
        case "email":
          this.user.email = event.value;
          this.errorMessage = event.errorMessage;
          break;
        case "company":
          this.user.company = event.value;
          this.errorMessage = event.errorMessage;
          break;
        case "employees":
          this.user.employees = event.value;
          this.errorMessage = event.errorMessage;
          break;
      }
    },

    handleSelected(value) {
      this.user.selected = value;
    },

    handleCheckTerm(event) {
      this.user.acceptTerm = event.target.checked;

      if (this.user.acceptTerm && this.checkTermMessage) {
        this.checkTermMessage = "";
      }

      if (
        this.user.acceptTerm &&
        this.user.name &&
        this.user.email &&
        this.user.company &&
        this.user.employees &&
        this.user.selected
      ) {
        this.steps[this.formActive - 1].validated = true;
      } else {
        this.steps[this.formActive - 1].validated = false;
      }
    },
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

  .check-term {
    text-align: left;
    padding-top: 20px;

    label {
      margin-left: 6px;
    }

    &__error {
      color: #aa4651;
      font-size: 12px;
      margin-top: 8px;
    }
  }
}
</style>
