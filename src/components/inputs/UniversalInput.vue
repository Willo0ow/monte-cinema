<template>
  <div class="input-wrapper">
    <label :for="name">{{ label }}</label>
    <div class="input-container">
      <img
        @click="showPassword = !showPassword"
        v-if="type === 'password'"
        class="icon"
        src="../../assets/eye.svg"
        alt="Show password icon"
      />
      <input
        :type="inputType"
        :name="name"
        :placeholder="placeholder"
        v-model="inputValue"
        @input="(event) => updateInputValue(event.target.value)"
        @blur="runInitialValidation"
        :class="{
          invalid:
            (useInputValidation || useStepValidation[activeStep]) && !isValid,
        }"
      />
    </div>
    <div class="messages-wrapper">
      <div
        class="message"
        v-for="(message, index) of messages"
        :key="`message-${index}`"
        :class="{
          'success-message': message.checkResult && message.checked,
          'error-message': !message.checkResult && message.checked,
        }"
      >
        {{ message.text }}
      </div>
    </div>
  </div>
</template>
<script>
import { computed, ref, watch, inject } from "vue";
export default {
  props: {
    name: { type: String, required: true },
    type: { type: String, default: "text" },
    placeholder: { type: String, default: "" },
    label: { type: String, default: "" },
    rules: { type: Array, default: () => [] },
  },
  setup(props) {
    const showPassword = ref(false);
    const inputType = computed(() => {
      return (props.type === "password" && showPassword.value) ||
        props.type === "date"
        ? "text"
        : props.type;
    });
    const inputValue = ref("");
    const valueLength = ref(0);
    const messages = computed(() => {
      if (props.rules.length) {
        return props.rules.map((rule) => {
          const checkResult = rule.check(inputValue.value);
          return {
            text: rule.message,
            checkResult,
            checked:
              !!inputValue.value ||
              useInputValidation.value ||
              useStepValidation[activeStep.value],
          };
        });
      }
      return [];
    });
    const useInputValidation = ref(false);
    const runInitialValidation = () => {
      useInputValidation.value = !isValid.value;
    };
    const isValid = computed(() => {
      if (props.rules.length) {
        return (
          inputValue.value.length &&
          messages.value.every(
            (message) => message.checkResult && message.checked
          )
        );
      }
      return inputValue.value.length > 0;
    });

    const activeStep = inject("activeStep");
    const setUserProperty = inject("setUserProperty");
    const validateUserProperty = inject("validateUserProperty");
    const useStepValidation = inject("useStepValidation");

    const updateInputValue = (value) => {
      if (props.type !== "date") {
        setUserProperty({ property: props.name, value });
      } else {
        updateDateValue(value);
      }
    };

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

    const updateDateValue = (date) => {
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
        inputValue.value =
          currentIndex === 0
            ? ""
            : `${date.slice(0, currentIndex)}${
                (correctDatePart.length === 2 ||
                  correctDatePart.length === 5) &&
                valueLength.value < date.length
                  ? "/"
                  : ""
              }`;
        valueLength.value = inputValue.value.length;
      }
    };

    watch(isValid, (newValidation) => {
      validateUserProperty({ property: props.name, isValid: newValidation });
    });

    return {
      messages,
      inputValue,
      isValid,
      runInitialValidation,
      useInputValidation,
      useStepValidation,
      showPassword,
      inputType,
      updateInputValue,
      activeStep,
    };
  },
};
</script>

<style scoped>
input {
  background: #f7f7f7;
  border-radius: 8px;
  border: 1px solid #f7f7f7;
  padding: 17.5px 24px;
  width: 100%;
  box-sizing: border-box;
}
input:hover {
  background: #e5e5e5;
}
input.invalid,
input.invalid:focus-visible {
  background: rgba(47, 128, 237, 0.1);
  outline: 1px solid #ec1115;
}
input:focus-visible {
  background: rgba(47, 128, 237, 0.1);
  outline: 1px solid #2f80ed;
}

::placeholder {
  color: #85868d;
}
.messages-wrapper {
  margin-top: 8px;
}
.message {
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
