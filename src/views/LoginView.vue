<template>
  <div class="container mt-5">
    <div class="mb-5 text-center">
      <h1 class="fw-light" style="color: #a6b7c9">Login</h1>
    </div>
    <form @submit.prevent="login" novalidate>
      <div class="row g-3">
        <div class="col-sm-6 mx-auto mb-3">
          <label for="username" class="form-label">Username</label>
          <input
            type="text"
            class="form-control"
            id="username"
            v-model="username"
          />
        </div>
      </div>
      <div class="row g-3">
        <div class="col-sm-6 mx-auto mb-3">
          <label for="password" class="form-label">Password</label>
          <input
            type="password"
            class="form-control"
            id="password"
            v-model="password"
          />
        </div>
      </div>
      <div class="row g-3">
        <div class="col-sm-6 mx-auto mb-3">
          <div v-if="msg" class="alert alert-danger" role="alert">
            {{ msg }}
          </div>
        </div>
      </div>
      <div class="row g-3">
        <div class="d-flex justify-content-center">
          <button class="btn btn-primary me-2 fw-bold" type="submit">
            Proceed
          </button>
          <button class="btn btn-outline-danger fw-bold" type="reset">
            Reset
          </button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "LoginView",
  data() {
    return {
      msg: "",
      input: {
        username: "",
        password: "",
      },
    };
  },
  methods: {
    login() {
      if (!this.username || !this.password) {
        this.msg = "Username and password are required.";
        return;
      } else if (this.username != "admin" || this.password != "admin") {
        this.msg = "Username or password is incorrect.";
      } else {
        this.$emit("authenticated", true);
        this.$root.setAuthenticated(true);
        this.$router.replace({ name: "home" });
      }
    },
  },
};
</script>
