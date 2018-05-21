<template>
    <div class="wrapper">
        <header-bar/>
        <main-bar/>
        <footer-bar/>
    </div>
</template>

<script>

import '@/assets/css/base/reset.css';
import '@/assets/css/fonts/iconfont.css';

import headerBar from './components/header';
import footerBar from './components/footer';
import mainBar from './components/main';

export default {
  name: 'App',
  components: {
    headerBar,
    mainBar,
    footerBar
  }
}
</script>

<style>
.wrapper {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
}
input {
    outline: none;
}
</style>
