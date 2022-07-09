<template>
  <div class="input-wrapper">
    <label :for="name">{{ label }}</label>
    <input
      :type="type"
      :name="name"
      :placeholder="placeholder"
      @input="(event) => checkRules(event)"
    />
    <div class="errors-wrapper">
      <div
        class="error"
        v-for="(error, index) of errors"
        :key="`error-${index}`"
      >
        {{ error.message }}
      </div>
    </div>
  </div>
</template>
<script>
import { computed } from "vue";
export default {
  props: {
    name: { type: String, required: true },
    type: { type: String, default: "text" },
    placeholder: { type: String, default: "" },
    label: { type: String, default: "" },
    rules: { type: Array, default: () => [] },
  },
  setup(props) {
    const errors = computed(() => {
      if (props.rules.length) {
        return [
          { message: "At least 8 characters" },
          { message: "At least one letter" },
          { message: "At least one digit" },
        ];
      }
      return [];
    });
    return {
      errors,
    };
  },
};
</script>

<style>
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
</style>
