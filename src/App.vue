<template>
 <TheBanner></TheBanner>
  <TheContent></TheContent>
</template>

<script>
import TheBanner from './components/TheBanner.vue';
import TheContent from './components/TheContent.vue';


export default {
  name: 'App',
  components: {
    TheBanner,
    TheContent
  }
}
</script>

<style>

</style>
