<template>
  <form action="/action_page.php" method="post" @submit.prevent="login">
    <div class="imgcontainer">
      <img
        src="https://www.w3schools.com/howto/img_avatar2.png"
        alt="Avatar"
        class="avatar"
      />
    </div>

    <div class="container">
      <label for="uname"
        ><b>{{ displayText.txt_userNameHeading }}</b></label
      >
      <input
        type="text"
        :style="[
          emailIsValid
            ? { 'border-color': 'black' }
            : { 'border-color': 'red' },
        ]"
        :placeholder="displayText.txt_userNamePlaceHolder"
        @blur="validateEmail"
        v-model="email"
        name="email"
        required
      />

      <label for="psw"
        ><b>{{ displayText.txt_passwordHeading }}</b></label
      >
      <input
        :style="[
          passwordIsValid
            ? { 'border-color': 'black' }
            : { 'border-color': 'red' },
        ]"
        type="password"
        :placeholder="displayText.txt_passwordPlaceHolder"
        @blur="validatePassword"
        v-model="password"
        name="psw"
        required
      />

      <button type="submit">Login</button>
      <label>
        <input type="checkbox" checked="checked" name="remember" /> Remember me
      </label>
    </div>

    <div class="container" style="background-color: #f1f1f1">
      <button type="button" class="cancelbtn">Cancel</button>
      <span class="psw">Forgot <a href="#">password?</a></span>
    </div>
  </form>
</template>
<script>
export default {
  name: "LoginForm",
  props: {},
  data() {
    return {
      displayText: {
        txt_userNameHeading: "Email",
        txt_userNamePlaceHolder: "Enter user email",
        txt_passwordHeading: "Password",
        txt_passwordPlaceHolder: "Enter the password",
      },
      password: "",
      passwordIsValid: true,
      email: "",
      emailIsValid: true,
    };
  },
  methods: {
    validatePassword() {
      this.passwordIsValid = this.$store.state.common.validatePassword(this.password);
    },
    validateEmail() {
      if (this.email.match(this.$store.state.common.emailCheckRegex)) {
        this.emailIsValid = true;
      } else {
        this.emailIsValid = false;
      }
    },
    login() {
      if (this.emailIsValid && this.passwordIsValid) {
        // submitting form only if both email and password is valid
      }
    },
  },
};
</script>
