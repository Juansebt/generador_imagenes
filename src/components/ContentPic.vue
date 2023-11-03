<template>
  <div class="container px-5">
    <hr class="mb-4">
    <form action="" class="mb-4">
      <div class="row g-2 mb-4">
        <div class="col-md">
          <div class="form-floating">
            <input type="number" class="form-control" id="floatingInputGrid" placeholder="Ancho de la foto" v-model="ancho_foto">
            <label for="floatingInputGrid" class="my-label">Ancho de la foto</label>
          </div>
        </div>
      </div>
      <div class="row g-2 mb-4">
        <div class="col-md">
          <div class="form-floating">
            <input type="number" class="form-control" id="floatingInputGrid" placeholder="Alto de la foto" v-model="alto_foto">
            <label for="floatingInputGrid" class="my-label">Alto de la foto</label>
          </div>
        </div>
      </div>
      <div class="row g-2 mb-4">
        <div class="col-md">
          <div class="form-floating">
            <select class="form-select" id="floatingSelect" aria-label="Floating label select example" v-model="blur_foto">
              <option selected>0</option>
              <option value="1">1</option>
              <option value="2">2</option>
              <option value="3">3</option>
              <option value="4">4</option>
              <option value="5">5</option>
              <option value="6">6</option>
              <option value="7">7</option>
              <option value="8">8</option>
              <option value="9">9</option>
              <option value="10">10</option>
            </select>
            <label for="floatingSelect">Agregar nivel de Blur</label>
          </div>
        </div>
      </div>
      <div class="row g-2">
        <div class="col-md">
          <div class="form-check">
            <input class="form-check-input" type="checkbox" value="" id="defaultCheck1" v-model="gray_foto">
            <label class="form-check-label" for="defaultCheck1">
              Activar Grayscale
            </label>
          </div>
        </div>
      </div>
      <br>
      <div class="mb-4 d-grid gap-2">
        <button type="button" class="btn btn-outline-primary" @click="get_foto">Generar Imagen</button>
      </div>
    </form>
    <hr>
    <Foto :imagenGenerada="imagenGenerada" class="mt-4"></Foto>
    <br>
  </div>
</template>

<script>
import axios from 'axios';
import Swal from 'sweetalert2'
import Foto from "./Foto.vue";

export default {
  components: {
    Foto,
  },
  data() {
    return {
      ancho_foto: '',
      alto_foto: '',
      blur_foto: 0,
      gray_foto: false,
      imagenGenerada: ''
    }
  },
  methods: {
    get_foto() {
      if (this.ancho_foto || this.alto_foto) {
        let url = `https://picsum.photos/${this.ancho_foto || this.alto_foto}/${this.alto_foto || this.ancho_foto}`;

        if (this.gray_foto) {
          url += '?grayscale';
        }

        if (this.blur_foto > 0 && this.blur_foto <= 10) {
          url += this.blur_foto ? `&blur=${this.blur_foto}` : `?blur=${this.blur_foto}`;
        }

        axios.get(url)
        .then(res => {
          this.imagenGenerada = res.config.url;
        })
        .catch(err => {
          Swal.fire({
            icon: 'error',
            title: 'Error',
            text: err,
          })
        });
      } else {
        Swal.fire({
          icon: 'error',
          title: 'Oops...',
          text: 'Por favor, ingresa valores para el ancho y alto de la imagen!',
        });
      }
    }
  },
  mounted(){}
};
</script>

<style>
label.my-label {
  opacity: 50%;
}
</style>
