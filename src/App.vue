<template>
  <div id="app">
    <Header />
    <router-view/>
  </div>
</template>

<script>
import Header from './components/layout/Header';
export default {
  name:"app",
  components: {
    Header
  }
}
</script>


<style>

body {
  margin-left: auto;
  margin-right: auto;
  max-width: 1000px;
}
</style>
