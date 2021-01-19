<template>
  <div class="profile">
    <div class="profile__user">
      <h3 class="profile__user-name">@{{ state.user.username }}</h3>
      <h2>{{ userId }}</h2>
      <div class="profile__user-tag" v-if="state.user.isAdmin">Admin</div>
      <div class="profile__user-followers">
        <strong>Followers:</strong> {{ state.followers }}
      </div>
    </div>
    <div class="profile__twoot-form">
      <createTwoot @emitTwoot="addTwoot" />
    </div>
    <!-- Twoots -->
    <div class="profile__user-twoots">
      <twoots
        v-for="twoot in state.user.twoots"
        v-bind:key="twoot.id"
        :username="state.user.username"
        :twoot="twoot"
      />
    </div>
  </div>
</template>

<script>
import { reactive, computed } from "vue";
import { useRoute } from "vue-router";
import { users } from "../assets/users.js";
import twoots from "@/components/Twoots";
import createTwoot from "@/components/CreateTwoot";

export default {
  name: "User Profile",

  components: {
    twoots,
    createTwoot,
  },

  setup() {
    const route = useRoute();
    const userId = computed(() => route.params.userId);
    const state = reactive({
      followers: 0,
      user: users[userId.value - 1] || users[0],
    });

    function addTwoot(twoot) {
      state.user.twoots.unshift({
        id: state.user.twoots.length + 1,
        content: twoot,
      });
    }

    return {
      state,
      addTwoot,
      userId,
    };
  },
};
</script>

<style lang="scss">
.profile {
  margin-top: 4rem;
  display: grid;
  grid-template-columns: repeat(2, 4fr);
  grid-auto-rows: minmax(min-content, max-content);
  justify-content: center;
  &__user {
    display: flex;
    flex-direction: column;
    justify-content: center;
    background: white;
    width: 30rem;
    padding: 2rem;
    &-tag {
      margin-top: 0.5rem;
      color: white;
      background: purple;
      font-size: 1.3rem;
      font-weight: 700;
      border-radius: 0.5rem;
      padding: 0 0.3rem;
      margin-right: auto;
    }
    &-followers {
      font-size: 1.4rem;
      margin-top: 1rem;
    }
    &-twoots {
      grid-column: 2 /3;
      grid-row: 1 / 3;
    }
  }
  &__twoot-form {
    grid-column: 1 / 2;
    grid-row: 2 / 3;
    margin: 1rem 0;
    background: white;
    padding: 1rem;
  }
}
</style>
