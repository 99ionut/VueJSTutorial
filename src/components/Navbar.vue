<template>
  <nav
    :class="[`bg-${theme}`, `navbar-${theme}`, 'navbar', 'container', 'navbar-expand-lg']"
  >
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li v-for="(page, index) in pages" class="nav-item active" :key="index">
          <navbar-link
            :page="page"
            :isActive="activePage === index"
            @click.prevent="navLinkClick(index)"
          >
          </navbar-link>
        </li>
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
  props: ["pages", "activePage", "navLinkClick"],
  data() {
    return {
      theme: "dark",
    };
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
