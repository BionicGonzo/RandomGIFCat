<template>
  <div id="app">
    <img id="gatoGIFhead" alt="Gato GIF" src="./assets/gato.gif">
    <GatosGIF msg="Random GIF Cat"/>
    <div class="seleccion">
      <p><label for="elTitulo">Título: </label><input name="elTitulo" id="elTitulo" type="text" v-model="titulo"></p>
      <div>
        <label for="elFiltro">Filtro:</label>
        <select v-model="filtro" name="elFiltro" id="elFiltro">
          <option value="blur">Blur</option>
          <option value="mono">Mono</option>
          <option value="sepia">Sepia</option>
          <option value="negative">Negative</option>
          <option value="paint">Paint</option>
          <option value="pixel">Pixel</option>
        </select>
      </div>
      <br>
      <div>
        <label for="elColor">Color:</label>
        <select v-model="color.background" name="elColor" id="elColor">
          <option value="green">Verde</option>
          <option value="yellow">Amarillo</option>
          <option value="blue">Azul</option>
          <option value="red">Rojo</option>
          <option value="orange">Naranja</option>
          <option value="pink">Rosa</option>
        </select>
        <br>
        <div class="muestra text-center m-auto" :style="color"></div>
      </div>
    <br>
    <p><label for="elTamano">Tamaño:</label> <input name="elTamano" id="elTamano" type="number" v-model="tamano"></p>
    <button type="button" class="btn btn-outline-light" @click="buscargato" data-bs-toggle="tooltip" data-bs-placement="right" title="Miau?">Obtener un gatito <i class="fa-solid fa-cat"></i></button>
    <br>
    <i id="flecha" class="fa-solid fa-angles-down"></i>
    </div>
    <GatosGIF :laImagen="urlImagen"/>
  </div>
</template>

<script>
import GatosGIF from './components/GatosGIF.vue'

export default {
  name: 'App',
  components: {
    GatosGIF
  },
  data() {
    return {
      titulo: '',
      filtro: '',
      tamano: '',
      urlImagen: '',
      color: {
        background: '',
      }
    }
  },
  methods: {
    buscargato() {
      let url = 'https://cataas.com/cat/gif/says/' + this.titulo + '?filter=' + this.filtro + '&color=' + this.color.background + '&size=' + this.tamano + '&type=or';
      fetch(url)
      .then(response => {
        // console.log(response);
        this.urlImagen = response.url;
      });
    },
  },
  created() {
    this.buscargato();
  } // Fin created
} // Fin export
</script>

<style>
body {
  background-color: #000;
  padding: 20px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #FFF;
  margin-top: 60px;
}

#gatoGIFhead {
  width: 30%;
  border-radius: 100%;
}

.seleccion {
  display: inline-block;
}

.muestra{
  width: 25px;
  height: 25px;
  border: 1px solid black;
  border-radius: 100%;
  margin-top: 20px !important;
}

input {
  width: 100%;
}

#flecha {
  padding: 20px;
  font-size: 50px;
}
</style>
