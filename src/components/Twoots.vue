<template>
  <div class="twoots">
    <div class="twoots__container" @click="faveTwoot(twoot.id)">
      <div class="twoots__user">@{{ userName }}</div>
      <div class="twoots__content">{{ twoot.content }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Twoot",
  props: {
    userName: {
      type: String,
      required: true,
    },
    twoot: {
      type: Object,
      required: true,
    },
  },
  methods: {
    faveTwoot(twootId) {
      this.$emit("fave", twootId);
    },
  },
};
</script>

<style lang="scss" scoped>
.twoots {
  display: flex;
  width: 100%;
  margin-left: 3rem;
  &:not(:first-child) {
    margin-top: 1rem;
  }
  &__container {
    background: white;
    padding: 2%;
    font-size: 1.8rem;
    width: 40vw;
    transition: all 0.25s ease;
    &:hover {
      transform: scale(1.1, 1.1);
    }
    cursor: pointer;
  }
  &__user {
    font-weight: 700;
  }
  &__content {
    margin-top: 1rem;
  }
}
</style>
