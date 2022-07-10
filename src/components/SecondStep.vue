<template>
  <div class="step-wrapper">
    <div class="title-wrapper">
      <content-title text="Great!" textColor="#343541"></content-title>
      <content-title text="Now your name" textColor="#85868d"></content-title>
    </div>
    <div class="form-wrapper">
      <form @submit="event.preventDefault()">
        <text-input
          v-for="(input, index) of inputs"
          :key="`input-${index}`"
          :label="input.label"
          :name="input.name"
          :type="input.type"
          :placeholder="input.placeholder"
          :rules="input.rules"
          @setValue="(value) => updateUserData({ property: input.name, value })"
        />
        <date-input
          label="Date of birth"
          name="dateOfBirth"
          placeholder="DD / MM / YYYY"
          @setValue="
            (value) => updateUserData({ property: 'dateOfBirth', value })
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
        />
        <div class="buttons-wrapper">
          <form-button label="Log in instead" :isPrimary="false"></form-button>
          <form-button
            label="Register"
            :action="() => setActiveTab('RegistrationSummary')"
          ></form-button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import { inject } from "vue";
import ContentTitle from "./ContentTitle.vue";
import FormButton from "./FormButton.vue";
import CustomCheckbox from "./inputs/CustomCheckbox.vue";
import TextInput from "./inputs/TextInput.vue";
import DateInput from "./inputs/DateInput.vue";
export default {
  name: "PageContent",
  components: {
    ContentTitle,
    TextInput,
    DateInput,
    FormButton,
    CustomCheckbox,
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
    const setActiveTab = inject("setActiveTab");
    return {
      inputs,
      updateUserData,
      setActiveTab,
      dateRules,
    };
  },
};
</script>
<style>
/* in app.css */
</style>
