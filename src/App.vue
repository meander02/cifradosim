<template>
  <div id="app">
    <h1>Cifrado AES</h1>
    <div class="contenedor-cifrado">
      <div class="contenedor-input">
        <label  for="texto">Texto a cifrar:</label>
        <input style="color: blue;" type="text" v-model="texto" id="texto" class="entrada-personalizada" />
      </div>
      <div class="contenedor-input">
        <label for="clave">Clave de cifrado:</label>
        <input style="color: rgb(33, 158, 75);" type="text" v-model="claveCifrado" id="clave" class="entrada-personalizada" />
      </div>
      <div class="contenedor-botones">
        <button @click="cifrar" class="boton-personalizado">Cifrar</button>
        <button @click="descifrar" class="boton-personalizado">Descifrar</button>
      </div>
      <div class="contenedor-resultado">
        <p style="color: rgb(210, 38, 172);" >Texto Cifrado: {{ textoCifrado }}</p>
        <p style="color: rgb(210, 38, 172);" >Texto Descifrado: {{ textoDescifrado }}</p>
      </div>
    </div>
  </div>
</template>

<script>

import CryptoJS from 'crypto-js';

export default {
  data() {
    return {
      texto: '',
      claveCifrado: '',
      textoCifrado: '',
      textoDescifrado: '',
    };
  },
  methods: {
    cifrar() {
      this.textoCifrado = CryptoJS.AES.encrypt(this.texto, this.claveCifrado).toString();
    },
    descifrar() {
      const bytes = CryptoJS.AES.decrypt(this.textoCifrado, this.claveCifrado);
      this.textoDescifrado = bytes.toString(CryptoJS.enc.Utf8);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  font-size: 2em;
  margin-bottom: 20px;
}

.contenedor-cifrado {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
}

.contenedor-input {
  text-align: left;
  margin: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  width: 100%;
  max-width: 400px;
}

.contenedor-input label {
  display: block;
  font-size: 1.2em;
  margin-bottom: 5px;
}

.entrada-personalizada {
  width: 80%;
  padding: 10px;
  font-size: 1em;
  border: none;
  border: 1px solid #3490dc;
  border-radius: 5px;
}

.contenedor-botones {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  gap: 10px;
}

.boton-personalizado {
  padding: 10px 20px;
  font-size: 1em;
  background-color: #3490dc;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.boton-personalizado:hover {
  background-color: #2779bd;
}

.contenedor-resultado {
  text-align: left;
}

@media (max-width: 768px) {
  .contenedor-cifrado {
    margin: 20px;
    
  }
}
</style>
