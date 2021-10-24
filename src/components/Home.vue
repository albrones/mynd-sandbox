<template lang="fr">
  <div>
    <h1>MyNd Sandbox</h1>
    <h3>My developer sandbox for experiment and have fun.</h3>
    <DailyRoutine/>
  </div>
</template>

<script>
import DailyRoutine from "./DailyRoutine.vue"

export default {
  name: "App",
  components: {
    DailyRoutine,
  },
}
</script>
<style lang="fr"></style>
