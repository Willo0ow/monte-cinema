<template>
  <div class="input-wrapper">
    <label :for="name">{{ label }}</label>
    <div class="input-container">
      <img
        v-if="type === 'password'"
        class="icon"
        src="../../assets/eye.svg"
        alt="Show password icon"
      />
      <input
        :type="type"
        :name="name"
        :placeholder="placeholder"
        v-model="value"
        @input="(event) => $emit('setValue', event.target.value)"
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
    type: { type: String, default: "text" },
    placeholder: { type: String, default: "" },
    label: { type: String, default: "" },
    rules: { type: Array, default: () => [] },
  },
  emits: ["setValue"],
  setup(props) {
    const value = ref("");
    const errors = computed(() => {
      if (props.rules.length) {
        return props.rules.map((rule) => {
          const checkResult = rule.check(value.value);
          return { message: rule.message, checkResult, checked: !!value.value };
        });
      }
      return [];
    });
    return {
      errors,
      value,
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
