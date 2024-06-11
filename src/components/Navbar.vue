<template>
  <nav
    :class="[`bg-${theme}`, `navbar-${theme}`, 'navbar', 'container', 'navbar-expand-lg']"
  >
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <navbar-link
          v-for="(page, index) in publishedPages"
          class="nav-item active"
          :key="index"
          :page="page"
          :index="index"
          :isActive="activePage === index"
        >
        </navbar-link>
      </ul>
    </div>
    <button @click="changeTheme">Change mode</button>
  </nav>
</template>

<script>
import NavbarLink from "./NavbarLink.vue";

export default {
  components: {
    NavbarLink,
  },
  created() {
    this.getThemeSettings();
  },
  props: ["pages", "activePage"],
  data() {
    return {
      theme: "dark",
    };
  },
  computed: {
    publishedPages() {
      return this.pages.filter((p) => p.published);
    },
  },
  methods: {
    changeTheme() {
      console.log("change theme");
      this.theme = this.theme == "light" ? "dark" : "light";
      this.storeThemeSettings();
    },
    storeThemeSettings() {
      localStorage.setItem("theme", this.theme);
    },
    getThemeSettings() {
      let theme = localStorage.getItem("theme");
      if (theme) {
        this.theme = theme;
      }
    },
  },
};
</script>
