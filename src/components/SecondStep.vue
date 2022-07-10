<template>
  <div class="step-wrapper">
    <div class="title-wrapper">
      <content-title text="Great!" textColor="#343541"></content-title>
      <content-title text="Now your name" textColor="#85868d"></content-title>
    </div>
    <div class="form-wrapper">
      <form>
        <form-input
          v-for="(input, index) of inputs"
          :key="`input-${index}`"
          :label="input.label"
          :name="input.name"
          :type="input.type"
          :placeholder="input.placeholder"
          :rules="input.rules"
        />
        <form-checkbox
          label="I accept Privacy Policy"
          name="policy"
          :rules="[]"
        />
        <div class="buttons-wrapper">
          <form-button label="Log in instead" :isPrimary="false"></form-button>
          <form-button label="Register"></form-button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
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
        name: "first",
        type: "text",
        placeholder: "e.g. Jessica ",
        rules: [],
      },
      {
        label: "Last name",
        name: "last",
        type: "text",
        placeholder: "e.g. Walton",
        rules: [],
      },
      {
        label: "Date of birth",
        name: "birthdate",
        type: "text",
        placeholder: "DD / MM / YYYY",
        rules: [1],
      },
    ];
    return {
      inputs,
    };
  },
};
</script>
<style>
/* in app.css */
</style>
