<template>
  <div class="page">
    <page-header></page-header>
    <div id="content">
      <component :is="activeTab"></component>
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
    const setActiveTab = (newTab) => (activeTab.value = newTab);
    provide("setActiveTab", setActiveTab);
    const userData = reactive({
      email: "",
      password: "",
      firstName: "",
      lastName: "",
      dateOfBirth: "",
      privacyPolicyAccepted: false,
    });
    const updateUserData = ({ property, value }) => {
      userData[property] = value;
    };
    provide("updateUserData", updateUserData);
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
