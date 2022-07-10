<template>
  <div class="step-wrapper">
    <div class="title-wrapper">
      <content-title
        :text="`Good job ${userData.firstName}!`"
        textColor="#343541"
      ></content-title>
    </div>

    <div class="message">
      <p>
        We have sent you an email to
        <strong>{{ userData.email }}</strong
        >.
      </p>
      <p>
        Make sure to click the link from the message to activate your account.
      </p>
    </div>
    <div class="button-wrapper">
      <form-button label="Go to homepage"></form-button>
    </div>
  </div>
</template>

<script>
import { inject } from "vue";
import ContentTitle from "./ContentTitle.vue";
import FormButton from "./FormButton.vue";
export default {
  name: "RegistrationSummary",
  components: { ContentTitle, FormButton },
  setup() {
    const userData = inject("userData");
    return {
      userData,
    };
  },
};
</script>

<style>
.button-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}
.message {
  font-family: "Roboto";
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 21px;
  text-align: center;
  color: #292a33;
  margin: 40px 0;
}
.message > p {
  margin: 0;
}
</style>
