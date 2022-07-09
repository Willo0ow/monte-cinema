<template>
  <div id="header">
    <img src="../assets/logo.svg" alt="logo" />
    <div id="slogan">
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
#header {
  height: 98px;
  padding: 25px 48px;
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: space-between;
  align-items: center;
  box-sizing: border-box;
}
#slogan {
  font-family: "Roboto Mono", monospace;
  font-size: 16px;
  text-transform: uppercase;
  letter-spacing: 0.03em;
}
.red-font {
  color: red;
}
</style>
