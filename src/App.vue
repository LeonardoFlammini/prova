<script>
import MainWrapper from "./components/MainWrapper.vue";
export default {
  name:"App",
  components:{
    MainWrapper
  }
}

</script>

<template>
  <header>
    <h1>Prova stampa</h1>
  </header>

  <main>
    <MainWrapper />
  </main>
</template>

<style lang="scss" scoped>
@import './scss/main.scss';

</style>
