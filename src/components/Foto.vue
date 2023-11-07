<template>
  <div class="container d-flex justify-content-center">
    <img :src="imagenGenerada" :style="imageStyle" alt="imagenGenerada">
  </div>
</template>

<script>
export default {
    props: {
        imagenGenerada: String,
        gray_foto: Boolean,
        foto_blur: Boolean,
    },
    computed: {
      imageStyle() {
        const styles = {};
        if (this.gray_foto) {
          styles.filter = 'grayscale(100%)';
        }
        if (this.foto_blur) {
          styles.filter = (styles.filter || '') + ' blur(3px)';
        }
        return styles;
      },
    },
}
</script>

<style>

</style>