<template>
  <div id="app">
    <Header />
    <Main />
    <Footer />
    <!-- <Popup /> -->
  </div>
</template>

<script>
import Header from './components/Header/Header'
import Main from './components/Main/Main'
import Footer from './components/Footer/Footer'
/* import Popup from './components/Popup/Popup' */

export default {
  name: 'App',
  components: {
    Header,
    Main,
    Footer
    /* Popup */
  }
}
</script>

<style>
@import url('../normalize.css');
@import url('../styles.css');
</style>
