<template>
  <div id="app">
    <TopBar/>
    <HeaderStripe/>

    <div class="page-wrapper">
      <transition name="fade" mode="out-in">
        <router-view/>
      </transition>
    </div>

    <SocialStripe/>
    <FooterSection/>
  </div>
</template>

<script>
import TopBar from '@/components/homepage/top-bar.vue'
import HeaderStripe from '@/components/homepage/header-stripe.vue'
import SocialStripe from '@/components/homepage/social-stripe.vue'
import FooterSection from '@/components/homepage/footer-section.vue'
import { mapActions } from "vuex";

import { FETCH_SESSIONIZE_DATA } from "@/store";

export default {
  components: {
    TopBar,
    HeaderStripe,
    SocialStripe,
    FooterSection,
  },
  created() {
    // * We can add other requests in the array as long as they can all be ran in parallel.
    const promises = [this.FETCH_SESSIONIZE_DATA()];
    Promise.all(promises).then(this.handleDataFetched);
  },

  methods: {
    ...mapActions([FETCH_SESSIONIZE_DATA]),

    handleDataFetched() {
      // * This can be changed to something more useful when required.
      console.log("Data fetched!");
    }
  }
};
</script>


<style lang="scss">
html,
body {
  min-height: 100%;
}

html {
  overflow-y: scroll;
  background-color: $color-main;
}

.fade-enter-active,
.fade-leave-active {
  transition-duration: 0.3s;
  transition-property: opacity;
  transition-timing-function: ease;
}

.fade-enter,
.fade-leave-active {
  opacity: 0;
}
</style>
