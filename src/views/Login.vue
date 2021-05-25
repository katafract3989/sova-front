<template>
  <div role="group" class="login-form">
    <!-- <h3>Log in to your account</h3> -->
    <img
      src="https://static.tildacdn.com/tild3633-3263-4536-b865-663337613130/Artboard.svg"
    />
    <br />
    <label class="input-live">Your phone number:</label>
    <b-form-input
      v-model="form.phone"
      placeholder="Phone"
      type="number"
    ></b-form-input>
    <small class="prompt-input">Minimum 5 characters. Required field</small>
    <br />
    <label class="input-live mt-3">Your password:</label>
    <b-form-input
      type="password"
      v-model="form.password"
      placeholder="Password"
    ></b-form-input>
    <small class="prompt-input">Minimum 6 characters. Required field</small>
    <br />
    <b-button block variant="outline-danger mt-4" @click="sendData"
      >Login</b-button
    >
    <div class="alert anim-show mt-5" v-if="error">{{ error }}</div>
  </div>
</template>

<script>
import Vue from "vue";
import axios from "axios";
import { BFormInput, FormInputPlugin, AlertPlugin } from "bootstrap-vue";
Vue.use(AlertPlugin);
Vue.use(FormInputPlugin);
Vue.component("b-form-input", BFormInput);
export default {
  data() {
    return {
      form: {
        phone: "",
        password: "",
      },
      error: "",
    };
  },

  methods: {
    sendData() {
      this.error = "";
      if (this.form.phone.length >= 4 && this.form.password.length >= 5) {
        axios
          .post("http://sova-back.ru/login", this.form, {
            headers: {
              "Content-Type": "application/json",
            },
          })
          .then((response) => (localStorage.token_session = response.data))
          .then(() => this.$router.push({ name: "Home" }))
          .catch((error) => {
            this.error = error.response.data;
          });
      } else {
        this.error =
          "Invalid data. Follow the guidelines for filling out the form. All fields are required!";
      }
    },
  },
};
</script>

<style scoped>
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  /* display: none; <- Crashes Chrome on hover */
  -webkit-appearance: none;
  margin: 0; /* <-- Apparently some margin are still there even though it's hidden */
}
.input-live {
  font-size: 18px;
}
input {
  text-align: center;
}
.prompt-input {
  text-align: left;
  opacity: 0.5;
  color: green;
}
.alert {
  border-left: 4px solid rgb(255, 136, 0);
  padding: 10px;
}
@media (max-width: 1200px) {
  .login-form {
    width: 95% !important;
    min-height: 100% !important;
  }
}
.login-form {
  background: #fff;
  padding: 0px 50px 50px 50px;
  border-radius: 18px;
  width: 30%;
  margin: auto;
}
.anim-show {
  opacity: 0;
  transition: 1s;
  animation: show 3s 1;
  animation-fill-mode: forwards;
}
@keyframes show {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}
</style>
