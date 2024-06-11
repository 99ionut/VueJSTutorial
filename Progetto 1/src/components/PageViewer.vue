<template>
  <div class="container" v-if="page">
    <h1 class="emphasize">Page Title</h1>
    <p>{{ $route.params.index }}</p>
  </div>
</template>

<script>
export default {
  created() {
    this.page = this.$pages.getSinglePage(this.$route.params.index);
  },
  data() {
    return {
      page: null,
    };
  },
};
</script>

<style scoped>
.emphasize {
  color: blue !important;
}
</style>
