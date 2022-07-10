<template>
  <step-content :inputs="inputs" :buttons="buttons" :title="title">
    <template #moreInputs>
      <date-input
        label="Date of birth"
        name="dateOfBirth"
        placeholder="DD / MM / YYYY"
        @setValue="
          (value) => updateUserData({ property: 'dateOfBirth', value })
        "
        @setValueValidation="
          (isValid) =>
            updateUserDataValidation({ property: 'dateOfBirth', isValid })
        "
        :rules="dateRules"
      ></date-input>
      <custom-checkbox
        label="I accept Privacy Policy"
        name="privacyPolicyAccepted"
        :rules="[]"
        @setValue="
          (value) =>
            updateUserData({ property: 'privacyPolicyAccepted', value })
        "
        @setValueValidation="
          (isValid) =>
            updateUserDataValidation({
              property: 'privacyPolicyAccepted',
              isValid,
            })
        "
      />
    </template>
  </step-content>
</template>

<script>
import { inject } from "vue";
import CustomCheckbox from "../components/inputs/CustomCheckbox.vue";
import DateInput from "../components/inputs/DateInput.vue";
import StepContent from "../components/StepContent.vue";
export default {
  name: "PageContent",
  components: {
    DateInput,
    CustomCheckbox,
    StepContent,
  },
  setup() {
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
    ];
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
    const updateUserData = inject("updateUserData");
    const updateUserDataValidation = inject("updateUserDataValidation");
    const setActiveTab = inject("setActiveTab");
    const title = [
      { text: "Great!", color: "#343541" },
      { text: "Now your name", color: "#85868d" },
    ];
    const buttons = [
      { label: "Log in instead", isPrimary: false, action: () => {} },
      {
        label: "Register",
        isPrimary: true,
        action: () => setActiveTab("RegistrationSummary"),
      },
    ];
    return {
      inputs,
      updateUserData,
      updateUserDataValidation,
      setActiveTab,
      dateRules,
      buttons,
      title,
    };
  },
};
</script>
