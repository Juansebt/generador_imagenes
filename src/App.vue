<template>
  <div class="container mt-3">
    <h1 class="text-center mb-4 mx-auto">Generador de imagenes</h1>
    <ContentPic></ContentPic>
  </div>
</template>

<script>
import {ref} from "vue";
import ContentPic from '@/components/ContentPic.vue'

export default {
  name: 'App',
  components: {
    ContentPic,
  }
}
</script>

<style lang="scss">

</style>
