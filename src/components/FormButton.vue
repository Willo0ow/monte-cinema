<template>
  <button
    :class="{ 'secondary-button': !isPrimary, 'primary-button': isPrimary }"
  >
    {{ label }}
  </button>
</template>

<script>
export default {
  props: {
    label: { type: String, default: "" },
    isPrimary: { type: Boolean, default: true },
    action: { type: Function, default: () => {} },
  },
};
</script>

<style>
button {
  font-family: "Roboto Mono";
  font-style: normal;
  font-weight: 500;
  font-size: 18px;
  line-height: 100%;
  letter-spacing: 0.015em;
  min-width: 228px;
  min-height: 56px;
  border: none;
  border-radius: 64px;
}
.primary-button {
  color: #ffffff;
  background: #ec1115;
}
.secondary-button {
  color: #ec1115;
  background: none;
}
</style>
