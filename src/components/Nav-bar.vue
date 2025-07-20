<template>
  <nav class="navbar navbar-expand-lg" style="background-color: #14181c">
    <div class="container-fluid">
      <router-link to="/home" class="navbar-brand">
        <img
          src="@/assets/cloneboxd.png"
          alt="Logo"
          width="206"
          height="24"
          class="d-inline-block align-text-top"
        />
      </router-link>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <router-link
              to="/"
              class="nav-link active fw-bold"
              @click="logout()"
              aria-current="page"
              style="color: #8faac7"
              >LOG OUT</router-link
            >
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: "NavBar",
  methods: {
    logout() {
      this.$root.logout();
    },
  },
};
</script>
