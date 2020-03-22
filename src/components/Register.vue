<template>
  <div class="container">
    <div class="row">
      <div class="col s12 m8 offset-m2">
        <div class="login card-panel green white-text center">
          <h3>Register</h3>
          <form>
            <div class="input-field">
              <i class="material-icons prefix">email</i>
              <input type="text" id="email" v-model="email" />
              <label class="white-text" for="email">Email</label>
            </div>
            <div class="input-field">
              <i class="material-icons prefix">email</i>
              <input type="password" id="password" v-model="password" />
              <label class="white-text" for="password">Password</label>
            </div>
          </form>

          <button @click.prevent="register" class="btn btn-large grey lighten-4 black-text">Register</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import firebase from "firebase/app";
import "firebase/auth";

export default {
  name: "register",
  data: function() {
    return {
      email: "",
      password: ""
    };
  },
  methods: {
    register: function() {
      firebase
        .auth()
        .createUserWithEmailAndPassword(this.email, this.password)
        .then(
          user => {
            alert(`Account created for ${user.user.email}`);
            this.$router.go({ path: this.$router.path });
          },
          err => alert(err.message)
        );
    }
  }
};
</script>