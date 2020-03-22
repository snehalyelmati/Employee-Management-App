<template>
  <nav>
    <div class="nav-wrapper blue">
      <div class="container">
        <router-link to="/" class="brand-logo">VueEpman</router-link>

        <ul class="right">
          <li v-if="isLoggedIn">
            <span class="email black-text">{{ currentUser }}</span>
          </li>

          <li v-if="isLoggedIn">
            <router-link to="/">Dashboard</router-link>
          </li>
          <li v-if="!isLoggedIn">
            <router-link to="/login">Login</router-link>
          </li>
          <li v-if="!isLoggedIn">
            <router-link to="/register">Register</router-link>
          </li>
          <li v-if="isLoggedIn">
            <button class="btn black" @click.prevent="logout">Logout</button>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import firebase from "firebase/app";
import "firebase/auth";

export default {
  name: "navbar",
  data() {
    return {
      isLoggedIn: false,
      currentUser: false
    };
  },
  created() {
    if (firebase.auth().currentUser) {
      (this.isLoggedIn = true),
        (this.currentUser = firebase.auth().currentUser.email);
    }
  },
  methods: {
    logout: function() {
      firebase
        .auth()
        .signOut()
        .then(
          () => {
            alert("Logged out!");
            this.$router.go({ path: this.$router.path });
          },
          err => alert(err.message)
        );
    }
  }
};
</script>

<style scoped>
.email {
  padding-right: 10px;
}
</style>