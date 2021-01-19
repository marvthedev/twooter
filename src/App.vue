<template>
  <div class="container">
    <router-view />
  </div>
</template>

<script>
export default {
  name: "Twootter",
};
</script>

<style lang="scss">
.container {
  display: flex;
  background: #f9f9f9;
  height: 100vh;
  padding: 0 25%;
}
</style>
