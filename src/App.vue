<template>
  <div id="app">
    <Header/>

    <div class="page-container">
      <div class="page-content">
        <Page/>
      </div>
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Page from './components/Page.vue';

export default {
  name: 'App',
  components: {
    Header,
    Page,
  },
};
</script>

<style lang="scss">
@import "./styles/reset.css";

#app {
  font-family: Lato, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #333;
  font-size: 16px;
}

* {
  box-sizing: border-box;
}

.page-container {
  padding: 0 16px;

  .page-content {
    max-width: 1024px;
    margin: auto;
  }
}
</style>
