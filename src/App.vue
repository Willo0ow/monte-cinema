<template>
  <div class="page">
    <page-header></page-header>
    <div id="content">
      <component :is="activeStep" />
    </div>
  </div>
</template>

<script>
import { reactive, ref, provide } from "vue";
import PageHeader from "./components/PageHeader.vue";
import FirstStep from "./steps/FirstStep.vue";
import SecondStep from "./steps/SecondStep.vue";
import RegistrationSummary from "./steps/RegistrationSummary.vue";
export default {
  name: "App",
  components: { PageHeader, FirstStep, SecondStep, RegistrationSummary },
  setup() {
    const activeStep = ref("FirstStep");
    provide("activeStep", activeStep);
    const useStepValidation = reactive({
      FirstStep: false,
      SecondStep: false,
      RegistrationSummary: false,
    });
    provide("useStepValidation", useStepValidation);

    const checkStepValidation = () => {
      return Object.keys(userData).reduce((isStepPropertiesValid, property) => {
        isStepPropertiesValid =
          userData[property].step === activeStep.value
            ? isStepPropertiesValid && userData[property].isValid
            : isStepPropertiesValid;
        return isStepPropertiesValid;
      }, true);
    };
    const setActiveTab = (newTab) => {
      const isStepFormValid = checkStepValidation();
      if (isStepFormValid) {
        activeStep.value = newTab;
      } else {
        useStepValidation[activeStep.value] = true;
      }
    };
    provide("setActiveTab", setActiveTab);
    const userData = reactive({
      email: { value: "", isValid: false, step: "FirstStep" },
      password: { value: "", isValid: false, step: "FirstStep" },
      firstName: { value: "", isValid: false, step: "SecondStep" },
      lastName: { value: "", isValid: false, step: "SecondStep" },
      dateOfBirth: { value: "", isValid: false, step: "SecondStep" },
      privacyPolicyAccepted: { value: "", isValid: false, step: "SecondStep" },
    });
    const setUserProperty = ({ property, value }) => {
      userData[property].value = value;
    };
    const validateUserProperty = ({ property, isValid }) => {
      userData[property].isValid = isValid;
    };
    provide("setUserProperty", setUserProperty);
    provide("validateUserProperty", validateUserProperty);
    provide("userData", userData);
    return {
      activeStep,
      useStepValidation,
    };
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
.page {
  width: 100%;
  height: 100%;
}
#content {
  height: calc(100vh - 98px);
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  box-sizing: border-box;
  min-height: 700px;
  position: relative;
  top: 98px;
}

@media (max-width: 602px) {
  #content {
    min-height: 600px;
  }
}
</style>
