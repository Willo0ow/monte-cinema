<template>
  <div id="content">
    <div style="border: 1px red solid">
      <div class="title-wrapper" style="border: 1px blue solid">
        <content-title text="Ahoy you!" textColor="#343541"></content-title>
        <content-title
          text="Care to register?"
          textColor="#85868d"
        ></content-title>
      </div>
      <div
        class="form-wrapper"
        style="border: 1px green solid; min-height: 200px"
      >
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
        </form>
      </div>
    </div>
  </div>
  :
</template>

<script>
import ContentTitle from "./ContentTitle.vue";
import FormInput from "./FormInput.vue";
export default {
  name: "PageContent",
  components: { ContentTitle, FormInput },
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
        rules: [1, 2, 3],
      },
    ];
    return {
      inputs,
    };
  },
};
</script>
<style scoped>
#content {
  height: calc(100vh - 98px);
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  box-sizing: border-box;
}
.form-wrapper {
  padding: 64px;
  box-sizing: border-box;
  margin-top: 40px;
}
</style>
