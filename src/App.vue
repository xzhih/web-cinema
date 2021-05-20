<template>
  <Home />
</template>

<script>
import Home from './components/Home';

export default {
  name: 'App',
  components: {
    Home
  }
};
</script>

<style>
body {
  font-size: 16px;
  color: #e6e6e6;
  background-color: #1d232b;
}


#app {
  font-family: -apple-system-font, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
:root {
  --plyr-color-main: #81d8d0;
}

@media screen and (max-width: 700px) {
  .plyr__menu__container [role='menu'] {
    overflow-y: scroll;
    max-height: calc((900vw / 16) - 130px);
  }

  .plyr__menu__container [role='menu']::-webkit-scrollbar {
    display: none;
  }
}

img[mode='aspectFill'] {
  object-fit: cover;
}

img[mode='widthFix'] {
  object-fit: scale-down;
}
</style>
