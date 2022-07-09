<template>
  <div class="page">
    <page-header></page-header>
  </div>
</template>

<script>
import PageHeader from "./components/PageHeader.vue";
export default {
  name: "App",
  components: { PageHeader },
};
</script>

<style>
.page {
  width: 100%;
  height: 100%;
}
</style>
