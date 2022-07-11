<template>
  <div class="step-wrapper">
    <div class="title-wrapper">
      <content-title
        v-for="(line, index) of title"
        :text="line.text"
        :textColor="line.color"
        :key="`title-line-${index}`"
      ></content-title>
    </div>
    <div class="form-wrapper">
      <form @submit.prevent>
        <universal-input
          v-for="(input, index) of inputs"
          :key="`input-${index}`"
          :label="input.label"
          :name="input.name"
          :type="input.type"
          :placeholder="input.placeholder"
          :rules="input.rules"
        />
        <slot name="moreInputs"></slot>
        <div class="buttons-wrapper">
          <form-button
            v-for="(button, idx) of buttons"
            :key="`form-button-${idx}`"
            :label="button.label"
            :isPrimary="button.isPrimary"
            :action="button.action"
          ></form-button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import ContentTitle from "./ContentTitle.vue";
import FormButton from "./FormButton.vue";
import UniversalInput from "./inputs/UniversalInput.vue";
export default {
  name: "FormWrapper",
  components: { ContentTitle, UniversalInput, FormButton },
  props: {
    inputs: { type: Array, required: true },
    buttons: { type: Array, required: true },
    title: { type: Array, required: true },
  },
  setup() {
    return {};
  },
};
</script>
<style scoped>
.form-wrapper {
  padding: 64px;
  box-sizing: border-box;
  margin-top: 40px;
  background: #ffffff;
  box-shadow: 0px 4px 22px rgba(52, 53, 65, 0.15);
  border-radius: 24px;
}

.buttons-wrapper {
  margin-top: 40px;
  display: flex;
  justify-content: space-between;
}

@media (max-width: 602px) {
  .buttons-wrapper {
    margin-top: 48px;
    display: flex;
    flex-direction: column;
    flex-flow: column-reverse;
    justify-content: center;
  }

  .form-wrapper {
    padding: 24px;
    margin-top: 48px;
    background: #ffffff;
    box-shadow: none;
  }
  .step-wrapper {
    padding: 24px;
    width: 100%;
  }
}
</style>
