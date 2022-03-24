<template>
  <Banner v-bind:style="cssProps"/>
  <div class="main-container">
    <h1>Dungeon Master's Realm</h1>
    <Dashboard />
  </div>
</template>

<script>
import Dashboard from "../components/Dashboard.vue"
import Banner from "../components/Banner.vue"
export default {
  name: "Administrative",
  components: {
    Dashboard,
    Banner
  },
  data() {
      return {
        cssProps: {
          backgroundImage: `url(${require("/public/img/cover3.jpg")})`
        }
      }
    }
}
</script>
