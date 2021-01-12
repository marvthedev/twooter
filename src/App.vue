<template>
  <div class="container">
    <userProfile />
  </div>
</template>

<script>
import userProfile from "@/components/UserProfile";

export default {
  name: "Twootter",
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
</style>
