<template>
  <div class="nav-container mb-3">
    <nav class="navbar navbar-expand-md navbar-light bg-light">
      <div class="container">
        <div class="navbar-brand logo"></div>
        <button
          class="navbar-toggler"
          type="button"
          data-toggle="collapse"
          data-target="#navbarNav"
          aria-controls="navbarNav"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>

        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav d-md-none" v-if="!isAuthenticated">
            <button class="btn btn-primary btn-block" @click="login">Log in</button>
          </ul>

          <ul class="navbar-nav d-md-none" v-if="isAuthenticated">
            <li class="nav-item">
              <span class="user-info">
                <img
                  :src="profile.picture"
                  alt="User's profile picture"
                  class="nav-user-profile d-inline-block"
                >
                <h6 class="d-inline-block">{{ profile.name }}</h6>
              </span>
            </li>
            <li>
              <span class="icon icon-profile"></span>
              <router-link to="/profile">Profile</router-link>
            </li>

            <li>
              <span class="icon icon-power"></span>
              <a id="qsLogoutBtn" href="/signout" class @click.prevent="logout">Log out</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  </div>
</template>

<script>
  export default {
    name: "NavBar",
    methods: {
      login() {
        this.$auth.login();
      },
      logout() {
        this.$auth.logOut();
        this.$router.push({ path: "/" });
      },
      handleLoginEvent(data) {
        this.isAuthenticated = data.loggedIn;
        this.profile = data.profile;
      }
    },
    data() {
      return {
        isAuthenticated: false,
        profile: {}
      };
    }
  };
</script>