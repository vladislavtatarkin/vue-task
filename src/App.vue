<template>
  <div id="app">
    <Navbar />
    <div class="container">
      <transition name="slide-fade" mode="out-in">
        <router-view :key="new Date()"/>
      </transition>
    </div>
  </div>
</template>

<script>
import Navbar from '@/components/Navbar'
export default {
  components: {Navbar}
}
</script>

<style lang="css">
  @import "~materialize-css/dist/css/materialize.min.css";

  .slide-fade-enter-active {
    transition: all .3s ease;
  }

  .slide-fade-leave-active {
    transition: all .3s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }

  .slide-fade-enter, .slide-fade-leave-active {
    padding-left: 10px;
    opacity: 0;
  }

</style>
