<template>
  <navbar :pages="pages" :active-page="activePage"></navbar>
  <router-view> </router-view>

  <!-- <page-viewer v-if="pages.length > 0" :page="pages[activePage]"> </page-viewer>
  <create-page @page-created="pageCreated"> </create-page> -->
</template>

<script>
import PageViewer from "./components/PageViewer.vue";
import Navbar from "./components/Navbar.vue";
import CreatePage from "./components/CreatePage.vue";

export default {
  components: {
    Navbar,
    PageViewer,
    CreatePage,
  },
  created() {
    this.getPages();

    this.$bus.$on("navbarLinkActivated", (index) => {
      this.activePage = index;
    });
  },
  data() {
    return {
      activePage: 0,
      pages: [],
    };
  },
  methods: {
    async getPages() {
      let res = await fetch("pages.json");
      let data = await res.json();

      this.pages = data;
    },
    pageCreated(pageObject) {
      console.log(pageObject);
      this.pages.push(pageObject);
    },
  },
};
</script>
