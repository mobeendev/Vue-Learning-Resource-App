<template>
  <the-header :title="HeaderTitle"></the-header>
  <stored-resources :resources="storedResources"></stored-resources>
  <the-resources></the-resources>
</template>

<script>
import TheResources from './components/TheResources.vue';
import TheHeader from './components/Layout/TheHeader.vue';

export default {
  components: {
    // StoredResources,
    TheHeader,
    TheResources,
  },
  data() {
    return {
      HeaderTitle: 'Remember Me',
    };
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

* {
  box-sizing: border-box;
}

html {
  font-family: 'Roboto', sans-serif;
}

body {
  margin: 0;
}
</style>
