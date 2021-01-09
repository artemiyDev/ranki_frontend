<template>
  <div>
    <b-form inline>
      <label class="sr-only" for="inline-form-input-username">Username</label>
      <b-input
        v-model="loginInfo.username"
        id="inline-form-input-username"
        class="mb-2 mr-sm-2 mb-sm-0"
        placeholder="Username"
      ></b-input>

      <label class="sr-only" for="text-password">Password</label>
      <b-input-group class="mb-2 mr-sm-2 mb-sm-0">
        <b-input
          v-model="loginInfo.password"
          type="password"
          id="text-password"
          placeholder="Password"
        ></b-input>
      </b-input-group>

      <b-form-checkbox class="mb-2 mr-sm-2 mb-sm-0">Remember me</b-form-checkbox>

      <b-button @click="loginUser(loginInfo)" variant="primary">Login</b-button>
    
    </b-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loginInfo: {
        username: "artem",
        password: "Zestaw87"
      }
    };
  },
  methods: {
    loginUser(loginInfo) {
      this.$auth.loginWith("local", {
        data: loginInfo
      });
    }
  }
};
</script>
