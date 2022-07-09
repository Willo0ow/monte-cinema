<template>
  <div class="page">
    <page-header></page-header>
    <page-content></page-content>
  </div>
</template>

<script>
import PageHeader from "./components/PageHeader.vue";
import PageContent from "./components/PageContent.vue";
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
</style>
