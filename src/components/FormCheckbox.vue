<template>
  <div class="checkbox-wrapper">
    <input type="checkbox" :value="true" :name="name" />
    <label :for="name">{{ label }}</label>
  </div>
</template>

<script>
export default {
  props: {
    name: { type: String, required: true },
    label: { type: String, default: "" },
    rules: { type: Array, default: () => [] },
  },
};
</script>

<style scoped>
label {
  font-family: "Roboto";
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 21px;
  color: #292a33;
  margin-left: 5px;
}
.checkbox-wrapper {
  margin-top: 24px;
}
</style>
