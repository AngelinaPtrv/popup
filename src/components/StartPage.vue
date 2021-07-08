<template>
  <div class="start__wrap">
    <button
        class="button-clear"
        @click="doVisiblePopup"
    >Налоговый вычет</button>
  </div>
</template>

<script>
export default {
  name: "StartPage",

  props: ['toVisible'],

  methods: {
    doVisiblePopup() {
      this.toVisible()
    }
  }
}
</script>

<style scoped>
.start__wrap {
  max-width: 100vw;
  height: 100vh;
  background: linear-gradient(255.35deg, #DC3131 0.83%, rgba(255, 79, 79, 0) 108.93%), #FF5E56;
  box-shadow: 0 -0.11px 16.9495px rgba(183, 187, 225, 0.33);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.button-clear {
  padding: 16px 32px;
}

</style>