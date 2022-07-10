<template>
  <div class="checkbox-wrapper">
    <input
      type="checkbox"
      value="agreed"
      :name="name"
      v-model="value"
      @change="(event) => updateValue(event.target.checked)"
    />
    <label :for="name">{{ label }}</label>
  </div>
</template>

<script>
import { ref } from "@vue/reactivity";
export default {
  props: {
    name: { type: String, required: true },
    label: { type: String, default: "" },
    rules: { type: Array, default: () => [] },
  },
  emits: ["setValue", "setValueValidation"],
  setup(props, context) {
    const value = ref(false);
    const updateValue = (newValue) => {
      context.emit("setValue", newValue);
      context.emit("setValueValidation", newValue);
    };
    return {
      value,
      updateValue,
    };
  },
};
</script>

<style scoped>
label {
  font-family: "Roboto";
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 21px;
  color: #292a33;
  margin-left: 5px;
}
.checkbox-wrapper {
  margin-top: 24px;
}
</style>
