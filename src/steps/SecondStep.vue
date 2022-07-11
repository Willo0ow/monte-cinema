<template>
  <step-content :inputs="inputs" :buttons="buttons" :title="title">
    <template #moreInputs>
      <custom-checkbox
        label="I accept <a href='#'>Privacy Policy<a/>"
        name="privacyPolicyAccepted"
        :rules="[{ check: (val) => !!val, message: 'Required' }]"
      />
    </template>
  </step-content>
</template>

<script>
import { inject } from "vue";
import CustomCheckbox from "../components/inputs/CustomCheckbox.vue";
import StepContent from "../components/StepContent.vue";
export default {
  name: "PageContent",
  components: {
    CustomCheckbox,
    StepContent,
  },
  setup() {
    const checkAge = (date) => {
      const [day, month, year] = date.split("/");
      let birthDate = new Date();
      birthDate.setDate(+day);
      birthDate.setMonth(+month - 1);
      birthDate.setFullYear(+year);
      let dateToCompare = new Date();
      dateToCompare.setFullYear(dateToCompare.getFullYear() - 18);
      return birthDate < dateToCompare;
    };
    const dateRules = [
      {
        check: (val) => checkAge(val),
        message: "You should be minium 18 years old",
      },
    ];
    const inputs = [
      {
        label: "First name",
        name: "firstName",
        type: "text",
        placeholder: "e.g. Jessica ",
        rules: [],
      },
      {
        label: "Last name",
        name: "lastName",
        type: "text",
        placeholder: "e.g. Walton",
        rules: [],
      },
      {
        label: "Date of birth",
        name: "dateOfBirth",
        type: "date",
        placeholder: "DD / MM / YYYY",
        rules: dateRules,
        maxlength: "10",
      },
    ];

    const setUserProperty = inject("setUserProperty");
    const validateUserProperty = inject("validateUserProperty");
    const setActiveTab = inject("setActiveTab");
    const register = () => {
      setActiveTab("RegistrationSummary");
    };
    const title = [
      { text: "Great!", color: "#343541" },
      { text: "Now your name", color: "#85868d" },
    ];
    const buttons = [
      {
        label: "Log in instead",
        isPrimary: false,
        action: () => {
          window.location.assign("#");
        },
      },
      {
        label: "Register",
        isPrimary: true,
        action: () => register(),
      },
    ];
    return {
      inputs,
      setUserProperty,
      validateUserProperty,
      setActiveTab,
      dateRules,
      buttons,
      title,
    };
  },
};
</script>
