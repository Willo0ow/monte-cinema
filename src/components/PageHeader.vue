<template>
  <div class="page-header">
    <img src="../assets/logo.svg" alt="logo" />
    <div class="slogan">
      Developed with <span class="red-font">♥</span> by Monterail
    </div>
  </div>
</template>

<script>
export default {
  name: "PageHeader",
};
</script>
<style scoped>
.page-header {
  height: 98px;
  padding: 25px 48px;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-between;
  align-items: center;
  box-sizing: border-box;
}
.slogan {
  font-family: "Roboto Mono", monospace;
  font-size: 16px;
  text-transform: uppercase;
  letter-spacing: 0.03em;
  font-weight: 500;
}
.red-font {
  color: red;
}
@media (max-width: 602px) {
  .slogan {
    display: none;
  }
  .page-header {
    justify-content: center;
  }
}
</style>
