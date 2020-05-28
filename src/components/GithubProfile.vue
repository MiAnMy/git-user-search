<template>
  <div id="profile">
    <div class="card">
      <div class="card-content">
        <div class="media">
          <div class="media-left">
            <figure class="image is-96x96">
              <img :src="info.avatar_url" alt="Avatar" />
            </figure>
          </div>
          <div class="media-content">
            <p class="title is-4">{{ info.name }}</p>
            <p class="subtitle is-6">{{ info.login }}</p>
          </div>
        </div>
        <div class="content">
          {{ info.bio }}
          <br />
          <time datetime="2016-1-1"
            >Created at: {{ formatTime(info.created_at) }}</time
          ><br />
          <time datetime="2016-1-1"
            >Last update: {{ formatTime(info.updated_at) }}</time
          >
        </div>
      </div>
      <footer class="card-footer">
        <p class="card-footer-item">Followers: {{ info.followers }}</p>
        <p class="card-footer-item">Following: {{ info.following }}</p>
      </footer>
      <footer class="card-footer">
        <p class="card-footer-item">Public repo: {{ info.public_repos }}</p>
      </footer>
    </div>
  </div>
</template>

<script>
export default {
  name: "Profile",
  props: {
    info: {
      type: Object,
      require: true,
    },
  },
  methods: {
    formatTime: function(time) {
      return new Date(time).toLocaleString();
    },
  },
};
</script>

<style></style>
