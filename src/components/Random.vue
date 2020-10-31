<template>
  <div>
    <div class="celeste1">
      <h1>Random Gif Cat</h1>
    </div>
    <div class="cherry">
      <form @submit.prevent="buscarGatito">
        <label for="texto">Titulo:</label> 
        <input type="text" name="texto" v-model="titulo">
        <label for="filtro">Filtro:</label> 
        <select name="filtro" v-model="filtro">
          <option value="blur">Blur</option>
          <option value="mono">Mono</option>
          <option value="sepia">Sepia</option>
          <option value="negative">Negative</option>
          <option value="paint">Paint</option>
          <option value="pixel">Pixel</option>
        </select>
        <label for="color">Color:</label>
        <select name="color" v-model="value" @change="circle(value)">
          <option value="red">Rojo</option>
          <option value="green">Verde</option>
          <option value="black">Negro</option>
          <option value="white">Blanco</option>
          <option value="blue">Azul</option>
        </select>
        <label for="size">Tamaño:</label>
        <input type="text" name="size" v-model="size">
        <button type="submit">Obtener mi gatito</button>
      </form>
      <div class="circle" :style="styleObject"></div>
    </div>
    <div class="celeste2">
      <img :src="gatitos" alt="">
    </div>
  </div>
</template>

<script>
export default {
  name: 'Random',
  data() {
    return {
      titulo: '',
      filtro: '',
      value: '',
      size: '',
      gatitos: '',
      styleObject: {
        backgroundColor: '',
      }
    }
  },
  methods: {
    buscarGatito(){
      fetch(`https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.value}&size=${this.size}`)
      .then(result => {
        this.gatitos = result.url;
      })
      .catch(error=> console.error(error)) 
    },

    circle(value) {
      if(value == 'red') {
        this.styleObject.backgroundColor = 'red';
      }

      if(value == 'green') {
        this.styleObject.backgroundColor = 'green';
      }

      if(value == 'black') {
        this.styleObject.backgroundColor = 'black';
      }

      if(value == 'white') {
        this.styleObject.backgroundColor = 'white';
      }

      if(value == 'blue') {
        this.styleObject.backgroundColor = 'blue';
      }
    }
  },
}
</script>


<style scoped>
form{
  display: flex;
  flex-direction: column;
  padding: 2em 21em;
  width: 50%;
}
label{
  padding-top: 1em;
}
button{
  margin-top: 1em;
  width: 18%;
  margin-left: 42%;
}
.celeste1{
  background-color: cadetblue;
  height: 150px;
}
.celeste2{
  background-color: cadetblue;
  height: 400px;
}
img{
  margin: 5em 35em;
}
.cherry{
  background-color: firebrick;
  height: 256px;
}
h1{
  font-size: 30px;
  font-weight: bolder;
  text-align: center;
  padding: 2em;
  margin: 0;
}
.circle {
  display: flex;
  border: 2px solid black;
  background-color: blanchedalmond;
  border-radius: 50%;
  width: 50px; 
  height: 50px;
  box-sizing: border-box;
  margin: -10em 17em 0em 64em;
}
</style>
