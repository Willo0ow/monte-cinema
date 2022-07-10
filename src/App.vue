<template>
  <div class="page">
    <page-header></page-header>
    <div id="content">
      <component :is="activeTab" />
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
    const activeTab = ref("FirstStep");
    const setActiveTab = (newTab) => {
      const isStepFormValid = Object.keys(userData).reduce(
        (allValid, property) => {
          allValid =
            userData[property].step === activeTab.value
              ? allValid && userData[property].isValid
              : allValid;
          return allValid;
        },
        true
      );
      if (isStepFormValid) {
        activeTab.value = newTab;
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
    const updateUserData = ({ property, value }) => {
      userData[property].value = value;
    };
    const updateUserDataValidation = ({ property, isValid }) => {
      userData[property].isValid = isValid;
    };
    provide("updateUserData", updateUserData);
    provide("updateUserDataValidation", updateUserDataValidation);
    provide("userData", userData);
    return {
      activeTab,
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
}
</style>
