<template>
  <div class="login">
    <h2></h2>
    <form @submit.prevent="onSubmit" class="loginform">
      <div>
        <label for="email">Email</label>
        <input class="form-control" type="text" name="email" 
          v-model="email" autofocus placeholder="e.g., test@test.com" />
      </div>
      <div>
        <label for="password">Passwrod</label>
        <input class="form-control" type="password" 
          v-model="password" placeholder="123123" />
      </div>
      <button  class="btn-login" :class="{'btn-success': !invalidForm}" type="submit" 
        :disabled="invalidForm">Log In</button>
    </form>
    <p class="error" v-if="error">{{error}}</p>
  </div>
</template>

<script>
import { mapActions } from "vuex";

export default {
  data() {
    return {
      email: "",
      password: "",
      error: "",
      rPath: ""
    };
  },
  computed: {
    invalidForm() {
      return !this.email || !this.password;
    }
  },
  created() {
    this.rPath = this.$route.query.rPath || "/";
  },
  methods: {
    ...mapActions(["LOGIN"]),
    onSubmit() {
      this.LOGIN({ email: this.email, password: this.password })
        .then(data => {
          this.$router.push(this.rPath);
        })
        .catch(err => {
          this.error = err.data.error;
        });
    }
  }
};
</script>

<style>
.login {
  width: 400px;
  height: 200px;
  padding: 50px;
  margin: 0 auto;
}
.loginform {
  padding: 30px;
  border-radius: 30px;
  background-color: white;
}
.btn-login {
  border-radius: 3px;
  padding: 6px 8px;
  border: none;
  display: inline-block;
  font-size: 14px;
  line-height: 20px;
  font-weight: 700;
  cursor: pointer;
  display: block;
  margin: auto;
  width: 200px;
  background-color: #ffdac0;
  color: black;
  box-shadow: none;
}
.error {
  color: #f00;
}
.form-control {
  border-top: none;
  border-left: none;
  border-right: none;
  border-bottom: 3px black;
  background-color: white;
}
</style>
