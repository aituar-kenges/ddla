<template>
  <div id="app">
    <Navbar />
    <div class="container">
      <router-view/>
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar';
import NewSite from './components/NewSite';

export default {
  name: 'app',
  components: {
    Navbar,
    NewSite
  }
};
</script>

<style>
nav {
  margin-bottom: 10px;
}
</style>
