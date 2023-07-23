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
@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");

body {
  height: 100vh;
  background: #121117;
  color: #e6e5ea;
  font-family: "Roboto", sans-serif;
  font-size: 20px;
}

h1 {
  text-align: center;
}

#password-app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 90vh;
}

@media only screen and (max-width: 500px) {
  body {
    font-size: 15px;
  }
}
</style>
