<template>
  <div class="form-control">
    <label :for="id"><slot></slot></label>
    <input
      :type="type"
      :id="id"
      @change="handleInput"
      @blur="handleValid"
      :placeholder="placeholder"
      :class="{ error: isError }"
    />
    <p class="message" v-if="isError">{{ errorMessage }}</p>
  </div>
</template>

<script>
export default {
  props: ["type", "id", "typeCustom", "placeholder", "isValid"],
  data() {
    return {
      errorMessage: "",
    };
  },
  computed: {
    isError() {
      return this.errorMessage.length !== 0 ? true : false;
    },
  },
  methods: {
    handleInput(event) {
      if (event.target.value) {
        this.errorMessage = "";
        this.$emit("input", event.target.value);
      }
    },
    handleValid(event) {
      const value = event.target.value;
      if (!value) {
        const textType = this.type.charAt(0).toUpperCase() + this.type.slice(1);
        this.errorMessage = `${textType} is required!`;
      } else {
        switch (this.type) {
          case "email":
            {
              const regex =
                /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
              if (!regex.test(value)) {
                this.errorMessage = "The field must be email!";
              }
            }
            break;
          case "text":
            if (this.typeCustom === "number") {
              if (Number(value)) {
                this.errorMessage = "Should be a valid value!";
              }
            }
            break;
        }
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.form-control {
  text-align: left;

  label {
    color: #000;
    font-size: 16px;
    display: block;
    margin-bottom: 6px;
  }

  input {
    color: #586068;
    font-size: 16px;
    width: 100%;
    padding: 8px 16px;
    border-radius: 4px;
    border: 1px solid #ccc;
    outline: 3px solid transparent;
    transition: all 0.2s ease;

    &.error {
      box-shadow: 0 0 4px #f4b6c1;
      border: 1px solid #aa4651;
    }

    &:focus {
      outline: 3px solid #c2d9fb;
      box-shadow: unset;
      border: 1px solid transparent;
    }
  }

  & + & {
    margin-top: 12px;
  }

  .message {
    color: #aa4651;
    font-size: 12px;
    margin-top: 8px;
  }
}
</style>
