<template>
  <Header></Header>
  <ImgArea />
</template>

<script>
import Header from '@/components/Header.vue'
import ImgArea from '@/components/ImgArea.vue'
export default {
  name: 'App',
  components: {
    ImgArea,
    Header
  },
  setup() {

  }
}
</script>

<style>
body {
  background-color: rgba(0, 0, 0, 0.725);
  margin: 0;
  padding: 0;
  position: relative;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: white;
}
</style>
