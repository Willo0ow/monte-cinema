<template>
  <h1 :style="{ color: textColor || 'inherit' }">{{ text }}</h1>
</template>

<script>
export default {
  name: "ContentTitle",
  props: {
    text: { type: String, required: true },
    textColor: { type: String, default: "" },
  },
};
</script>

<style>
h1 {
  font-size: 80px;
  font-family: "Eczar", serif;
  font-weight: 600;
  line-height: 102%;
  /* or 82px */
  letter-spacing: -0.01em;
  margin: 0;
}
@media (max-width: 600px) {
  h1 {
    font-size: 40px;
    text-align: center;
  }
}
</style>
