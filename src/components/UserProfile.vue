<template>
  <div class="profile">
    <div class="profile__user">
      <h3 class="profile__user-name">@{{ user.userName }}</h3>
      <div class="profile__user-tag" v-if="user.isAdmin">Admin</div>
      <div class="profile__user-followers">
        <strong>Followers:</strong> {{ followers }}
      </div>

      <!-- Twoots -->
    </div>
    <div class="profile__user__twoots">
      <twoots
        v-for="twoot in user.twoots"
        v-bind:key="twoot.id"
        :username="user.userName"
        :twoot="twoot"
      />
    </div>
  </div>
</template>

<script>
import twoots from "./Twoots";

export default {
  name: "User Profile",
  components: {
    twoots,
  },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        userName: "devvelox",
        firstName: "Marvin",
        lastName: "Marinas",
        email: "devveloxofficial@gmail.com",
        isAdmin: true,
        twoots: [
          {
            id: 1,
            content: "Twooter is so fun!",
          },
          {
            id: 2,
            content: "Don't forget to subscribe!",
          },
        ],
      },
    };
  },

  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.userName} has gained a follower!`);
      }
    },
  },

  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`;
    },
  },

  methods: {
    addFollower() {
      this.followers++;
    },
  },

  mounted() {
    this.addFollower();
  },
};
</script>

<style lang="scss">
.profile {
  display: flex;
  &__user {
    display: flex;
    flex-direction: column;
    justify-content: center;
    background: white;
    height: 10rem;
    margin-top: 4rem;
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
      margin-top: 0.7rem;
    }
  }
}
</style>
