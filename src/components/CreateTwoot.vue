<template>
  <form action="" class="create-twoot" @submit.prevent="createNewTwoot">
    <label for="create-twoot__content" class="create-twoot__content-label"
      >New Twoot <span>({{ twootCharacterCount }}/180)</span></label
    >
    <textarea
      id="create-twoot__content"
      class="create-twoot__content"
      rows="4"
      v-model="state.newTwootContent"
    ></textarea>
    <div class="create-twoot__type">
      <label for="create-twoot__type-select" class="create-twoot__type-label"
        >Type:</label
      >
      <select
        id="create-twoot__type-select"
        class="create-twoot__type-select"
        v-model="state.selectedTwootType"
      >
        <option
          :value="option.value"
          v-for="(option, index) in state.twootTypes"
          :key="index"
          >{{ option.name }}</option
        >
      </select>
    </div>
    <button class="create-twoot__btn">Twoot!</button>
  </form>
</template>

<script>
import { reactive, computed } from "vue";

export default {
  name: "Create Twoot",

  setup(props, ctx) {
    const state = reactive({
      newTwootContent: "",
      selectedTwootType: "instant",
      twootTypes: [
        {
          value: "draft",
          name: "Draft",
        },
        {
          value: "instant",
          name: "Instant Twoot",
        },
      ],
    });

    const twootCharacterCount = computed(() => state.newTwootContent.length);

    function createNewTwoot() {
      if (state.newTwootContent && state.selectedTwootType !== "draft") {
        ctx.emit("emitTwoot", state.newTwootContent);
        state.newTwootContent = "";
      }
    }

    return {
      state,
      twootCharacterCount,
      createNewTwoot,
    };
  },
};
</script>

<style lang="scss" scoped>
.create-twoot {
  display: flex;
  flex-direction: column;
  &__content {
    margin-top: 1rem;
    border: 0.1rem solid#e8e8e8;
    width: 100%;
    &-label {
      font-size: 1.8rem;
      font-weight: 700;
      & span {
        font-weight: 400;
      }
    }
  }
  &__type {
    margin-top: 1rem;
    &-label {
      font-size: 1.6rem;
      font-weight: 700;
    }
    &-select {
      margin-left: 1rem;
      border: 0.1rem solid#e8e8e8;
    }
  }
  &__btn {
    margin: 1rem 0 0 auto;
  }
}
</style>
