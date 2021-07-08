<template>
  <div id="app" class="start">
    <start-page
        :toVisible='toVisible'
        v-if="!popupVisible"
    ></start-page>
    <popup
        :toVisible="toVisible"
        v-if="popupVisible"></popup>
  </div>
</template>

<script>

import Popup from "@/components/Popup";
import StartPage from "@/components/StartPage";

export default {
  name: 'App',

  components: {
    Popup,
    StartPage
  },

  data() {
    return {
      popupVisible: false
    }
  },

  methods: {
    toVisible() {
      this.popupVisible = !this.popupVisible;
    }
  }
}
</script>

<style>
@import "~@/assets/css/reset.css";
@import "~@/assets/css/styles.css";
@import "~@/assets/fonts/fonts.css";
</style>
