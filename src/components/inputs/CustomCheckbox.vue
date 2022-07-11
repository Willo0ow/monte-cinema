<template>
  <div class="checkbox-wrapper">
    <input
      type="checkbox"
      value="agreed"
      :name="name"
      v-model="value"
      @change="(event) => updateValue(event.target.checked)"
      :class="{ error: useStepValidation[activeStep] && !value }"
    />
    <label class="checkbox-label" :for="name" v-html="label"></label>
  </div>
</template>

<script>
import { ref, inject } from "vue";
export default {
  props: {
    name: { type: String, required: true },
    label: { type: String, default: "" },
    rules: { type: Array, default: () => [] },
  },
  setup(props) {
    const value = ref(false);
    const setUserProperty = inject("setUserProperty");
    const validateUserProperty = inject("validateUserProperty");
    const updateValue = (newValue) => {
      setUserProperty({ property: props.name, value: newValue });
      validateUserProperty({ property: props.name, isValid: newValue });
    };
    const activeStep = inject("activeStep");
    const useStepValidation = inject("useStepValidation");
    return {
      value,
      updateValue,
      useStepValidation,
      activeStep,
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
checkbox-label > a {
  color: #292a33 !important;
}
.checkbox-wrapper {
  margin-top: 24px;
}

input.error[type="checkbox"]:not(:disabled) {
  box-shadow: 0px 0px 1px 1px #ff03038c, inset 0px 0px 1px 1px #ff03038c;
}
</style>
