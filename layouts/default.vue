<template>
  <div class="mainbody">
    <Header class="no-flex-grow" />
    <b-container fluid class="flex-grow  mt-4">
      <nuxt />
    </b-container>
    <Footer class="no-flex-grow" />
  </div>
</template>
<style scoped>
  .mainbody {
    height: 100vh;
    display: flex;
    flex-direction: column;
  }
  .no-flex-grow {
    flex-grow: 0;
  }
  .flex-grow {
    flex: 1;
  }
</style>
<script>
import Header from '~/components/Header'
import Footer from '~/components/Footer'
export default {
  components: {
    Header,
    Footer
  }
}
</script>
