<template>
  <div class="container px-5">
    <hr class="mb-4">
    <div class="row">
      <div class="col-md-6 col-12 mb-4">
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
                <input type="number" class="form-control" id="floatingInputGrid" placeholder="Nivel de Blur" v-model="blur_foto">
                <label for="floatingInputGrid" class="my-label">Nivel de Blur</label>
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
            <div class="col-md">
              <div class="form-check">
                <input class="form-check-input" type="checkbox" value="" id="defaultCheck2" v-model="foto_blur" :disabled="blur_foto !== ''">
                <label class="form-check-label" for="defaultCheck2">
                  Activar Blur
                </label>
              </div>
            </div>
          </div>
          <br>
          <div class="mb-4 d-grid gap-2">
            <button type="button" class="btn btn-outline-primary" @click="get_foto">Generar Imagen</button>
          </div>
        </form>
      </div>
      <div class="col-md-6 col-12">
        <Foto :imagenGenerada="imagenGenerada" :gray_foto="gray_foto" :foto_blur="foto_blur"></Foto>
      </div>
    </div>
    <br>
  </div>
  <br>
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
      blur_foto: '',
      gray_foto: false,
      foto_blur: false,
      imagenGenerada: ''
    }
  },
  methods: {
    get_foto() {
      if (this.ancho_foto || this.alto_foto) {
        const randomTime = new Date().getTime();
        let url = `https://picsum.photos/${this.ancho_foto || this.alto_foto}/${this.alto_foto || this.ancho_foto}`;

        if (this.blur_foto) {
          const blurLevel = parseInt(this.blur_foto);
          if (blurLevel >= 1 && blurLevel <= 10) {
            url += `?blur=${blurLevel}`;
          } else {
            Swal.fire({
              icon: 'error',
              title: 'Error',
              text: 'El nivel de blur debe estar en el rango de 1 a 10.',
            });
            this.blur_foto = '';
            return;
          }
        }

        if (this.gray_foto) {
          url += `?grayscale`;
        }
        
        url += `?${randomTime}`;

        console.log(url);
        
        axios.get(url)
        .then(res => {
          Swal.fire({
            icon: 'success',
            title: 'Imagen generada con éxito',
            showConfirmButton: false,
            timer: 1500, 
          });
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
