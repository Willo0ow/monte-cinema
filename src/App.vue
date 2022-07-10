<template>
  <div class="page">
    <page-header></page-header>
    <div id="content">
      <page-content></page-content>
    </div>
  </div>
</template>

<script>
import PageHeader from "./components/PageHeader.vue";
import PageContent from "./components/SecondStep.vue";
export default {
  name: "App",
  components: { PageHeader, PageContent },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
.page {
  width: 100%;
  height: 100%;
}
#content {
  height: calc(100vh - 98px);
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  box-sizing: border-box;
}
</style>
