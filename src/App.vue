<template>
  <div class="container">
    <userProfile />
  </div>
</template>

<script>
import userProfile from "./components/UserProfile";

export default {
  name: "2weeter",
  components: {
    userProfile,
  },
};
</script>

<style lang="scss">
.container {
  display: flex;
  background: #f9f9f9;
  height: 100vh;
  padding: 0 25%;
}

//CSS Reset & Defaults
html {
  font-size: 62.5%;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  border: none;
}

body {
  color: #3e3e3e;
  font-weight: 400;
  font-family: "Zilla Slab", serif;
}

input {
  outline: 0;
  border-radius: 0;
}

b,
strong,
h1,
h2 {
  font-weight: 700;
}

a {
  text-decoration: none;
}

ul {
  list-style: none;
}
h1 {
  font-size: 4rem;
}
h2 {
  font-size: 3rem;
}

h3 {
  font-size: 2.8rem;
  font-weight: 700;
}

p {
  font-size: 2.1rem;
  font-weight: 300;
  line-height: 150%;
  margin-bottom: 0.5rem;
}

a {
  text-decoration: none;
}

input,
textarea {
  font-family: inherit;

  //Remove unwanted thick border-top on iOS devices
  background-clip: padding-box;
}

textarea {
  resize: none;
  border-radius: 0;
}
</style>
