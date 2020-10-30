<template>
  <div>
    <div class="celeste">
      <h1>Random Gif Cat</h1>
    </div>
    <div class="cherry">
      <form  @submit.prevent="buscarGatito">
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
        <select name="color" v-model="value">
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
    </div>
    <div class="celeste">
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
      gatitos: ''
    }
  },
  methods: {
    buscarGatito(){
      fetch(`https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.value}&size=${this.size}`)
      .then(result => {
        this.gatitos = result.url;
        console.log(this.value)
      })
      .catch(error=> console.error(error)) 
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
}
.celeste{
  background-color: cadetblue;
  height: 150px;
}
.cherry{
  background-color: firebrick;
}
h1{
  font-size: 30px;
  font-weight: bolder;
  text-align: center;
  padding-top: 2em;
}
</style>
