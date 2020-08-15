<template>
  <div id="app">
    <div class="logo">
      <img src="./assets/logo.png" alt="logo" class="logo" />
    </div>
    <section>
      <h1 class="heading">WeJapa Country Directory</h1>
    </section>
    <CountryDirectory />
  </div>
</template>

<script>
import CountryDirectory from "@/views/CountryDirectory.vue";
export default {
  components: {
    CountryDirectory
  }
};
</script>
<style lang="scss">
body {
  margin: 0;
  padding: 0;
}
#app {
  background: url("./assets/04754_HD.jpg");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  opacity: 0.8;
}
.logo {
  text-align: center;
  height: 5rem;
}
.heading {
  text-align: center;
  font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
    "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
  color: rgb(76, 133, 184);
  margin: 2rem 0;
}
</style>
