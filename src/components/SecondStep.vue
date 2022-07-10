<template>
  <div class="step-wrapper">
    <div class="title-wrapper">
      <content-title text="Great!" textColor="#343541"></content-title>
      <content-title text="Now your name" textColor="#85868d"></content-title>
    </div>
    <div class="form-wrapper">
      <form @submit="event.preventDefault()">
        <form-input
          v-for="(input, index) of inputs"
          :key="`input-${index}`"
          :label="input.label"
          :name="input.name"
          :type="input.type"
          :placeholder="input.placeholder"
          :rules="input.rules"
          @setValue="(value) => updateUserData({ property: input.name, value })"
        />
        <form-checkbox
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
import FormCheckbox from "./FormCheckbox.vue";
import FormInput from "./FormInput.vue";
export default {
  name: "PageContent",
  components: { ContentTitle, FormInput, FormButton, FormCheckbox },
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
      {
        label: "Date of birth",
        name: "dateOfBirth",
        type: "text",
        placeholder: "DD / MM / YYYY",
        rules: [1],
      },
    ];
    const updateUserData = inject("updateUserData");
    const setActiveTab = inject("setActiveTab");
    return {
      inputs,
      updateUserData,
      setActiveTab,
    };
  },
};
</script>
<style>
/* in app.css */
</style>
