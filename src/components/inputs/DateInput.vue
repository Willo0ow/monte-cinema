<template>
  <div class="input-wrapper">
    <label :for="name">{{ label }}</label>
    <div class="input-container">
      <input
        type="text"
        :name="name"
        :placeholder="placeholder"
        maxlength="10"
        v-model="value"
        @input="(event) => updateValue(event.target.value)"
      />
    </div>
    <div class="errors-wrapper">
      <div
        class="error"
        v-for="(error, index) of errors"
        :key="`error-${index}`"
        :class="{
          'success-message': error.checkResult && error.checked,
          'error-message': !error.checkResult && error.checked,
        }"
      >
        {{ error.message }}
      </div>
    </div>
  </div>
</template>
<script>
import { computed, ref } from "vue";
export default {
  props: {
    name: { type: String, required: true },
    placeholder: { type: String, default: "" },
    label: { type: String, default: "" },
    rules: { type: Array, default: () => [] },
  },
  emits: ["setValue"],
  setup(props, context) {
    const value = ref("");
    const errors = computed(() => {
      if (props.rules.length) {
        return props.rules.map((rule) => {
          if (value.value.length === 10) {
            const checkResult = rule.check(value.value);
            return { message: rule.message, checkResult, checked: value.value };
          } else {
            return {
              message: rule.message,
              checkResult: false,
              checked: false,
            };
          }
        });
      }
      return [];
    });
    const dateRegexByLength = [
      /[0-3]/,
      /0[1-9]|[1][0-9]|[2][0-9]|3[01]/,
      /0[1-9]|[1][0-9]|[2][0-9]|3[01]\//,
      /(0[1-9]|[1][0-9]|[2][0-9]|3[01])\/[0-1]/,
      /(0[1-9]|[1][0-9]|[2][0-9]|3[01])\/(0[1-9]|1[0-2])/,
      /(0[1-9]|[1][0-9]|[2][0-9]|3[01])\/(0[1-9]|1[0-2])\//,
      /(0[1-9]|[1][0-9]|[2][0-9]|3[01])\/(0[1-9]|1[0-2])\/[1-2]/,
      /(0[1-9]|[1][0-9]|[2][0-9]|3[01])\/(0[1-9]|1[0-2])\/19|20/,
      /(0[1-9]|[1][0-9]|[2][0-9]|3[01])\/(0[1-9]|1[0-2])\/19[0-9]|20[0-2]/,
      /(0[1-9]|[1][0-9]|[2][0-9]|3[01])\/(0[1-9]|1[0-2])\/(19[0-9][0-9]|20[0-1][0-9])/,
    ];
    const updateValue = (date) => {
      if (date.length) {
        const length = date.length;
        let isCorrect = true;
        let currentIndex = 0;
        while (isCorrect && currentIndex <= length - 1) {
          if (dateRegexByLength[currentIndex].test(date)) {
            currentIndex += 1;
          } else {
            isCorrect = false;
          }
        }
        const correctDatePart = date.slice(0, currentIndex);
        value.value =
          currentIndex === 0
            ? ""
            : `${date.slice(0, currentIndex)}${
                correctDatePart.length === 2 || correctDatePart.length === 5
                  ? "/"
                  : ""
              }`;
      }
      context.emit("setValue", value.value);
    };
    return {
      errors,
      value,
      updateValue,
    };
  },
};
</script>

<style scoped>
input {
  background: #f7f7f7;
  border-radius: 8px;
  border: none;
  padding: 17.5px 24px;
  width: 100%;
  box-sizing: border-box;
}
::placeholder {
  color: #85868d;
}
.errors-wrapper {
  margin-top: 8px;
}
.error {
  font-family: "Roboto";
  font-style: normal;
  font-weight: 400;
  font-size: 14px;
  line-height: 170%;
  letter-spacing: 0.04em;
  color: #343541;
}
label {
  font-family: "Roboto Mono";
  font-style: normal;
  font-weight: 700;
  font-size: 14px;
  line-height: 18px;
  text-transform: uppercase;
  display: block;
  color: #f47073;
  margin-bottom: 12px;
}
.input-container {
  position: relative;
  width: 100%;
  display: flex;
  align-items: center;
}
.icon {
  position: absolute;
  right: 24px;
  min-width: 18px;
  text-align: center;
}
.success-message {
  color: #27ae60;
}
.error-message {
  color: #ec1115;
}
</style>
