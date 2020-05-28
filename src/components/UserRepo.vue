<template>
  <div id="userepo">
    <div class="card">
      <header class="card-header">
        <p class="card-header-title">
          {{ data.name }}
        </p>
        <a
          class="card-header-icon"
          aria-label="more options"
          @click="moreOption = !moreOption"
        >
          <span class="icon">
            <i class="fas fa-angle-down" aria-hidden="true"></i>
          </span>
        </a>
      </header>
      <div class="card-content" v-if="moreOption">
        <div class="content">
          <p>
            {{ data.description || "No description" }}
          </p>
        </div>
      </div>
      <footer class="card-footer">
        <p class="card-footer-item" title="Language" v-show="data.language">
          {{ data.language }}
        </p>
      </footer>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserRepo",
  data: () => ({
    moreOption: false,
  }),
  props: {
    data: {
      type: Object,
      require: true,
    },
  },
};
</script>

<style></style>
