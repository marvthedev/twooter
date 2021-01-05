<template>
  <div class="twoots">
    <div class="twoots__content">{{ twoot.content }}</div>
  </div>
</template>

<script>
export default {
  name: "Twoot",
  props: {
    username: {
      type: String,
      required: true,
    },
    twoot: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="scss">
.twoots {
  display: flex;
  &__content {
    background: white;
    padding: 2%;
    margin-top: 2rem;
  }
}
</style>
