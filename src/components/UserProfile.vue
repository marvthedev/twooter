<template>
  <div class="profile">
    <div class="profile__user">
      <h3 class="profile__user-name">@{{ user.userName }}</h3>
      <div class="profile__user-tag" v-if="user.isAdmin">Admin</div>
      <div class="profile__user-followers">
        <strong>Followers:</strong> {{ followers }}
      </div>
      <form
        action=""
        class="profile__twoot-form"
        @submit.prevent="createNewTwoot"
      >
        <label for="profile__new-twoot-input" class="profile__new-twoot-title"
          >New Twoot <span>({{ characterCount }}/180)</span></label
        >
        <textarea
          id="profile__new-twoot-input"
          class="profile__new-twoot-input"
          rows="4"
          v-model="newTwootContent"
        ></textarea>
        <div class="profile__new-twoot-type">
          <label
            for="profile__new-twoot-type-select"
            class="profile__new-twoot-type-title"
            >Type:</label
          >
          <select
            id="profile__new-twoot-type-select"
            class="profile__new-twoot-type-select"
            v-model="selectedTwootType"
          >
            <option
              :value="option.value"
              v-for="(option, index) in twootTypes"
              :key="index"
              >{{ option.name }}</option
            >
          </select>
        </div>
        <button>Twoot!</button>
      </form>
    </div>
    <!-- Twoots -->
    <div class="profile__user-twoots">
      <twoots
        v-for="twoot in user.twoots"
        v-bind:key="twoot.id"
        :userName="user.userName"
        :twoot="twoot"
        @fave="toggleFavourite"
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
      newTwootContent: "",
      selectedTwootType: "instant",
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
    characterCount() {
      return this.newTwootContent.length;
    },
  },

  methods: {
    addFollower() {
      this.followers++;
    },
    toggleFavourite(id) {
      console.log(`Favorited Tweet #${id}`);
    },
    createNewTwoot() {
      if (this.selectedTwootType !== "draft" && this.newTwootContent !== "") {
        this.user.twoots.unshift({
          id: this.user.twoots.length + 1,
          content: this.newTwootContent,
        });
        this.newTwootContent = "";
      }
    },
  },

  mounted() {
    this.addFollower();
  },
};
</script>

<style lang="scss">
.profile {
  margin-top: 4rem;
  display: flex;
  justify-content: center;
  &__user {
    display: flex;
    flex-direction: column;
    justify-content: center;
    background: white;
    height: 50%;
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
      margin-top: 0.7rem;
    }
  }
  &__twoot-form {
    display: flex;
    flex-direction: column;
    margin: 1rem 0;
    border-top: 0.1rem solid#e8e8e8;
    padding-top: 1rem;
  }

  &__new-twoot {
    &-title {
      font-size: 1.8rem;
      font-weight: 700;
      & span {
        font-weight: 400;
      }
    }
    &-input {
      margin-top: 1rem;
      border: 0.1rem solid#e8e8e8;
    }
    &-type {
      margin-top: 0.5rem;
      &-title {
        font-size: 1.6rem;
        font-weight: 700;
      }
      &-select {
        margin-left: 1rem;
        border: 0.1rem solid#e8e8e8;
      }
    }
  }
}
</style>
