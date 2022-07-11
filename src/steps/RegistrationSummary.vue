<template>
  <div class="step-wrapper" style="padding: 24px">
    <div class="title-wrapper">
      <content-title
        :text="`Good job ${userData.firstName.value}!`"
        textColor="#343541"
        textAlign="center"
      ></content-title>
    </div>

    <div class="summary-message">
      <p>
        We have sent you an email to
        <strong>{{ userData.email.value }}</strong
        >.
      </p>
      <p>
        Make sure to click the link from the message to activate your account.
      </p>
    </div>
    <div class="button-wrapper">
      <form-button label="Go to homepage" @click="goToHomepage"></form-button>
    </div>
  </div>
</template>

<script>
import { inject } from "vue";
import ContentTitle from "../components/ContentTitle.vue";
import FormButton from "../components/FormButton.vue";
export default {
  name: "RegistrationSummary",
  components: { ContentTitle, FormButton },
  setup() {
    const userData = inject("userData");
    const goToHomepage = () => window.location.assign("#");
    return {
      userData,
      goToHomepage,
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
.summary-message {
  font-family: "Roboto";
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 21px;
  text-align: center;
  color: #292a33;
  margin: 40px 0;
}
.summary-message > p {
  margin: 0;
}
</style>
