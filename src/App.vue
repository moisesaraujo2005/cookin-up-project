<template>
 <TheBanner></TheBanner>
  <TheContent>

  </TheContent>
  <TheFooter></TheFooter>
</template>

<script>
import TheBanner from './components/TheBanner.vue';
import TheContent from './components/TheContent.vue';
import TheFooter from './components/TheFooter.vue';


export default {
  name: 'App',
  components: {
    TheBanner,
    TheContent,
    TheFooter
  }
}
</script>

<style>

</style>
