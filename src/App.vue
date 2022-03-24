<template>
  <div>
    <Navbar :logo="logo_src" />
    <div>
      <router-view></router-view>
    </div>
    <Footer />
  </div>
</template>
<script>
import Navbar from './components/Navbar'
import Footer from './components/Footer'
export default {
  data: function() {
    return {
      logo_src: "/img/logo.png",
    }
  },
  components: {
    Navbar,
    Footer
  }
}
</script>

<style>
  * {
    font-family: "Draconis";
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container {
    margin: 50px;
    min-height: 250px;
  }
  
  h1 {
    font-family: "DND-Title";
    text-align: center;
    font-size: 42px;
    margin-top: 30px;
    margin-bottom: 30px;
    color: #222;
  }

  @font-face {
    font-family: "DND-Title";
    src: url("../public/fonts/Breathe-Fire.ttf") format("truetype");
  }
  
  @font-face {
    font-family: "DND-Text";
    src: url("../public/fonts/Draconis.ttf") format("truetype");
  }
</style>