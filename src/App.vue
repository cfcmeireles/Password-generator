<template>
  <main id="password-app">
    <div>
      <h1>Password Generator</h1>
      <p>
        Tired of being asked for multiple requirements so that you can create a
        lengthy and secure password?
      </p>
      <p>We're here to help! Generate your new totally safe password here!</p>
      <PasswordGenerator />
    </div>
  </main>
</template>

<script>
import PasswordGenerator from "./components/PasswordGenerator.vue";
export default {
  name: "App",
  components: {
    PasswordGenerator,
  },
};
</script>

<style></style>
