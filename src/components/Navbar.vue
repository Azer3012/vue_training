<template>
  <nav
    :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']"
  >
    <div class="container-fluid">
      <a href="#" class="navbar-brand">My Vue</a>
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <navbar-link
          v-for="(page, index) in publishedPage"
          :key="index"
          class="nav-item"
          :page="page"
          
          :index="index"
          
        >
        </navbar-link>

        <li>
          <router-link to="/pages/create" aria-current="page" class="nav-link" active-class="active">Create Page</router-link>
        </li>
      </ul>
      <form class="d-flex">
        <button class="btn btn-primary" @click.prevent="changeTheme()">
          Toggle theme navbar
        </button>
      </form>
    </div>
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
    this.pages=this.$pages.getAllPages();
  },

  computed: {
    publishedPage() {
      return this.pages.filter((page) => page.published);
    },
  },

  data() {
    return {
      theme: "light",
      pages:[]
    };
  },
  methods: {
    changeTheme() {
      let theme = "light";
      if (this.theme == "light") {
        theme = "dark";
      }
      this.theme = theme;
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
