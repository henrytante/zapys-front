<template>
  <div class="header">
    <h2>ZAPYS - Painel</h2>
  </div>
  <div class="container">
    <select v-model="selectedEndpoint">
      <option value="escolha" style="display: none;" disabled hidden>Escolha:</option>
      <option value="nome">Nome - V1</option>
      <option value="placa">Placa - V1</option>
      <option value="cpf">CPF - V1</option>
      <option value="cpfv2">CPF - V2</option>
      <option value="cep">CEP - V1 (lento)</option>
    </select>

    <div class="components">
      <input type="text" v-model="token" placeholder="Token: ">
      <input type="text" v-model="dado" placeholder="Insira aqui: ">
      <button @click="requestData">Enviar</button>
    </div>

    <div v-if="responseData">
      <pre>{{ responseData }}</pre>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      selectedEndpoint: 'escolha',
      token: '',
      placa: '',
      responseData: null
    };
  },
  methods: {
    async requestData() {
      let apiUrl = '';

      if (this.selectedEndpoint === 'nome') {
        apiUrl = `https://api.zapys.xyz/api/v1/nome?token=${this.token}&nome=${this.dado}`;
      } else if (this.selectedEndpoint === 'placa') {
        apiUrl = `https://api.zapys.xyz/api/v1/placa?token=${this.token}&placa=${this.dado}`;
      } else if (this.selectedEndpoint === 'cpf') {
        apiUrl = `https://api.zapys.xyz/api/v1/cpf?token=${this.token}&cpf=${this.dado}`;
      } else if (this.selectedEndpoint === 'cpfv2') {
        apiUrl = `https://api.zapys.xyz/api/v2/cpf?token=${this.token}&cpf=${this.dado}`;
      } else if (this.selectedEndpoint === 'cep') {
        apiUrl = `https://api.zapys.xyz/api/v1/cep?token=${this.token}&cep=${this.dado}`;
      }
       else {
        console.log("outro");
      }

      try {
        const response = await axios.get(apiUrl, {
          maxRedirects: 0, // Define o número de redirecionamentos para 0
          validateStatus: function (status) {
            return status >= 200 && status < 400; // Valida apenas se o status for entre 200 e 399
          },
        });
        this.responseData = response.data;
        
      } catch (error) {
        this.responseData = "não encontrado"
      }
    }
  }
};
</script>
 <style>
:root {
  font-family: Inter, system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;

  color-scheme: light dark;
  color: rgba(255, 255, 255, 0.87);
  background-color: #242424;

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.components{
  display: flex;
  flex-direction: column;
  margin: 10px;
}

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  text-align: center;
}

.header{
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: rgba(255, 255, 0, 0.849);
  color: black;
  text-align: center;
  z-index: 999;
}
.container{
  position: relative;
  display: flex;
  flex-direction: column;
  margin-bottom: 10px;
}
button {
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 0.6em 1.2em;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  background-color: #1a1a1a;
  cursor: pointer;
  transition: border-color 0.25s;
}
input {
  border-radius: 8px;
  border: 0.03rem solid yellow;
  padding: 0.6rem 1.2rem;
  margin-bottom: 15px;
  font-size: 1em;
  font-weight: 500px;
  font-family: inherit;
  background-color: #1a1a1a;
  outline: none;  
}
button:hover {
  border-color: yellow;
}
button:focus,
button:focus-visible {
  outline: 4px auto -webkit-focus-ring-color;
}
body {
  display: flex;
  place-items: center;
  min-width: 320px;
  min-height: 100vh;
}
select {
  background-color: #1a1a1a;
  color: yellow;
  padding: 8px;
  padding: 0.6rem 1.2rem;
  border: 0.03rem solid yellow;
  border-radius: 8px;
  outline: none;
  cursor: pointer;
  font-weight: bold;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
  width: calc(100% - 24px); 
  margin: 0 auto; 
}
select section .escolha{
  display: none;
}
select::-ms-expand {
  display: none;
}
select:hover{
  border-color: yellow;
}
select:focus {
  border-color: yellow;
}
</style>