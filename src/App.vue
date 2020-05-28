<template>
  <div id="app">
    <div class="columns ">
      <div class="column is-one-third is-offset-one-third">
        <div class="field">
          <label class="label">Github profile:</label>
          <div :class="'control ' + [profileLoading && 'is-loading']">
            <input
              class="input"
              type="text"
              placeholder="..."
              @keyup.enter="
                findUser();
                $event.target.blur();
              "
              v-model="profileName"
            />
          </div>
        </div>
      </div>
    </div>
    <div class="columns" v-if="profile">
      <div class="column is-one-third is-offset-one-third">
        <github-profile :info="profile" />
      </div>
    </div>
    <user-repo
      v-for="repo in repos"
      class="column is-one-third is-offset-one-third"
      v-show="repos"
      :key="repo.id"
      :data="repo"
    />
  </div>
</template>

<script>
import GithubProfile from "./components/GithubProfile";
import UserRepo from "./components/UserRepo";

export default {
  name: "App",
  data: () => ({
    profile: null,
    repos: null,
    profileLoading: false,
    profileName: null,
  }),
  methods: {
    findUser: function() {
      this.profileLoading = true;
      fetch(`https://api.github.com/users/${this.profileName}`)
        .then((response) => {
          if (!response.ok) {
            this.profileLoading = false;
            if (response.status === 404) this.profileName = "404";
            throw new Error(response.status);
          }
          return response.json();
        })
        .then((json) => {
          this.profile = json;
          console.log(this.profile);
          this.showRepos();
        });
    },
    showRepos: function() {
      fetch(`https://api.github.com/users/${this.profile.login}/repos`)
        .then((response) => response.json())
        .then((json) => {
          this.repos = json;
          this.profileLoading = false;
        });
    },
  },
  components: { GithubProfile, UserRepo },
};
</script>

<style></style>
