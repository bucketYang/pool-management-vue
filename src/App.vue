<template>
  <div id="app" class="overflow-hidden">
    <UiLoading v-if="ui.loading || !ui.init" class="overlay big" />
    <div v-else>
      <Topnav />
      <div
        class="d-flex flex-row pb-6"
        :style="ui.sidebarIsOpen && 'max-height: 100vh'"
      >
        <div
          class="shell d-block d-xl-none"
          :class="ui.sidebarIsOpen && 'sidebar-is-open'"
          @click="toggleSidebar"
        />
        <Sidebar :key="$router.currentRoute.fullPath" />
        <router-view id="view" class="flex-auto" />
      </div>
    </div>
    <Notifications />
  </div>
</template>

<script>
import { mapActions } from 'vuex';

// import Router from 'vue-router';

// const originalPush = Router.prototype.push;
// Router.prototype.push = function push(location, onResolve, onReject) {
//   if (onResolve || onReject)
//     return originalPush.call(this, location, onResolve, onReject);
//   return originalPush.call(this, location).catch(err => err);
// };

export default {
  watch: {
    $route() {
      this.hideSidebar();
    }
  },
  methods: {
    ...mapActions(['init', 'toggleSidebar', 'hideSidebar'])
  },
  mounted() {
    // const x = GIT_DESCRIBE;
    this.init();
  }
};
</script>

<style lang="scss">
@import './vars';

#view {
  margin-left: 0;
  margin-top: 80px;

  @media (min-width: $width-xl) {
    margin-left: 264px;
  }
}

.shell {
  &.sidebar-is-open {
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.4);
  }
}
</style>
