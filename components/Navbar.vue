<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="#">Ranki</b-navbar-brand>
      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item to="/decks">Decks</b-nav-item>
          <b-nav-item to="/about">About</b-nav-item>
        </b-navbar-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <div v-if="$auth.loggedIn">
            <b-navbar-nav>
              <b-nav-item to="/profile">{{ $auth.user }}</b-nav-item>
              <b-nav-item @click="logOut()">Logout</b-nav-item>
            </b-navbar-nav>
          </div>
          <div v-else>
            <b-navbar-nav>
              <b-nav-item to="/login">Login</b-nav-item>
              <b-nav-item to="/register">Register</b-nav-item>
            </b-navbar-nav>
          </div>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  methods: {
    logOut() {
      this.$auth.logout();
    }
  }
};
</script>
