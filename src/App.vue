<template>
  <div id="db-wrapper">
    <!-- navbar vertical -->
    <!-- Sidebar -->
    <nav class="navbar-vertical navbar">
      <div class="nav-scroller">
        <!-- Brand logo -->
        <router-link class="navbar-brand" to="/">
          <LogoComponent />
        </router-link>
        <!-- Navbar nav -->
        <ul class="navbar-nav flex-column" id="sideNavbar">
          <li class="nav-item">
            <router-link class="nav-link has-arrow" :to="{ name: 'home' }">
              <i class="fa-solid fa-house nav-icon icon-xs me-2"></i> Home
            </router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link has-arrow" :to="{ name: 'taskList' }">
              <i class="fa-solid fa-list nav-icon icon-xs me-2"></i> To Do
            </router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" :to="{ name: 'createTask' }">
              <i class="fa-solid fa-plus nav-icon icon-xs me-2"></i> Assign Task
            </router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" :to="{ name: 'createTeam' }">
              <i class="fa-solid fa-users nav-icon icon-xs me-2"></i> Teams
            </router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" :to="{ name: 'login' }">
              <i class="fa-solid fa-lock-open nav-icon icon-xs me-2"></i> Login
            </router-link>
          </li>
          <li class="nav-item">
            <a href="#" class="nav-link">
              <button class="btn btn-danger" @click="handleLogout">
                Logout
              </button>
            </a>
          </li>
        </ul>
      </div>
    </nav>
    <!-- Page Content -->
    <div id="page-content">
      <router-view />
    </div>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>

<script>
import { mapActions } from "vuex";
import LogoComponent from "../src/components/LogoComponent.vue";

export default {
  components: { LogoComponent },
  methods: {
    ...mapActions({
      logout: "auth/logout",
    }),
    handleLogout() {
      this.logout();
      if (this.$route.name !== "login") {
        this.$router.push("/login");
      }
    },
  },
};
</script>
