<template>
  <div class="container d-flex justify-content-center">
    <img :src="imagenGenerada" alt="imagenGenerada">
  </div>
</template>

<script>
export default {
    props: {
        imagenGenerada: '',
    },
}
</script>

<style>

</style>