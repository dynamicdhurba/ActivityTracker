<template lang="pug">
div#wrapper
  aw-header

  div(:class="{'container': !fullContainer, 'container-fluid': fullContainer}")
    div.aw-container.my-3.p-3
      error-boundary
        user-satisfaction-poll
        new-release-notification(v-if="isNewReleaseCheckEnabled")
        router-view

  div.container(style="color: #555")
    div(style="float: left")
      div.mb-1
        div 

    div(style="float: right; text-align: right;")
      |  #[a(href="https://github.com/ActivityWatch/activitywatch/issues/new")]
      br
      | #[a(href="https://forum.activitywatch.net/c/support")]
      br
      | #[a(href="https://forum.activitywatch.net/c/features")]
      br
      | #[a(href="https://forum.activitywatch.net/c/projects")]
      br
      span.mt-2(v-show="info", style="color: #888; font-size: 0.8em")
        | Host: {{info.hostname}}
</template>

<script>
// only import the icons you use to reduce bundle size
import 'vue-awesome/icons/brands/twitter';
import 'vue-awesome/icons/brands/github';

export default {
  data: function () {
    return {
      activityViews: [],
      info: {},
      isNewReleaseCheckEnabled: !process.env.VUE_APP_ON_ANDROID,
    };
  },

  computed: {
    fullContainer() {
      return this.$route.meta.fullContainer;
    },
  },

  mounted: async function () {
    this.$aw.getInfo().then(
      info => {
        this.info = info;
      },
      e => {
        console.error('Unable to connect: ', e);
        this.info = {};
      }
    );
  },
};
</script>

