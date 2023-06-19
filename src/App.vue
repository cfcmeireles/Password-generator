<template>
  <main id="password-app">
    <div>
      <h1>Password Generator</h1>
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

<style>
body {
  height: 100vh;
  background: #121117;
  color: #e6e5ea;
}

h1 {
  text-align: center;
}
</style>
