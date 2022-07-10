<template>
  <step-content
    :inputs="inputs"
    :buttons="buttons"
    :title="title"
  ></step-content>
</template>

<script>
import { inject } from "vue";
import StepContent from "../components/StepContent.vue";
export default {
  name: "FirstStep",
  components: { StepContent },
  setup() {
    const inputs = [
      {
        label: "Email",
        name: "email",
        type: "email",
        placeholder: "Something ending with monterail.com",
        rules: [],
      },
      {
        label: "Password",
        name: "password",
        type: "password",
        placeholder: "Enter your password",
        rules: [
          { check: (val) => val.length >= 8, message: "At least 8 characters" },
          {
            check: (val) => /[a-zA-Z]/.test(val),
            message: "At least one letter",
          },
          { check: (val) => /\d/.test(val), message: "At least one digit" },
        ],
      },
    ];
    const title = [
      { text: "Ahoy you!", color: "#343541" },
      { text: "Care to register?", color: "#85868d" },
    ];
    const setActiveTab = inject("setActiveTab");
    const buttons = [
      { label: "Log in instead", isPrimary: false, action: () => {} },
      {
        label: "Next Step",
        isPrimary: true,
        action: () => setActiveTab("SecondStep"),
      },
    ];
    const updateUserData = inject("updateUserData");
    return {
      inputs,
      updateUserData,
      setActiveTab,
      title,
      buttons,
    };
  },
};
</script>
