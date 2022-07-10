<template>
  <div class="step-wrapper">
    <div class="title-wrapper">
      <content-title text="Ahoy you!" textColor="#343541"></content-title>
      <content-title
        text="Care to register?"
        textColor="#85868d"
      ></content-title>
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
        <div class="buttons-wrapper">
          <form-button label="Log in instead" :isPrimary="false"></form-button>
          <form-button
            label="Next Step"
            :action="() => setActiveTab('SecondStep')"
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
import TextInput from "./inputs/TextInput.vue";
export default {
  name: "PageContent",
  components: { ContentTitle, TextInput, FormButton },
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
