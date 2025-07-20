<template>
  <Navbar v-if="authenticated"></Navbar>
  <router-view />
</template>

<style>
.btn.btn-primary {
  background-color: #15ad2d !important;
  border-color: #15ad2d !important;
}
.btn.btn-primary:hover {
  background-color: #1fbf3a !important;
  border-color: #1fbf3a !important;
}
.btn.btn-primary:active {
  background-color: #0f8a23 !important;
  border-color: #0f8a23 !important;
}
</style>

<script>
import Navbar from "@/components/Nav-bar.vue";

export default {
  components: {
    Navbar,
  },
  data() {
    return {
      authenticated: false,
    };
  },
  mounted() {
    if (this.authenticated == false) {
      this.$router.replace({ name: "login" });
    }
  },
  methods: {
    setAuthenticated(status) {
      this.authenticated = status;
    },
    logout() {
      this.authenticated = false;
      this.$router.replace({ name: "login" });
    },
  },
};
</script>
