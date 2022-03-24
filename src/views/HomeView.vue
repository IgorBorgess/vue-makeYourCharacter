<template>
  <div>
    <Banner v-bind:style="cssProps"/>
    <div class="main-container">
      <h1>Build your Character:</h1>
      <CharacterForm />
    </div>
  </div>
</template>

<script>
import Banner from '../components/Banner.vue'
import CharacterForm from '../components/CharacterForm.vue'
export default {
  name: 'Home',
  components: {
    Banner,
    CharacterForm
  },
  data() {
    return {
    cssProps: {
      backgroundImage: `url(${require('/public/img/cover2.jpg')})`
      }
    }
  }
}
</script>