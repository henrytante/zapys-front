<template>
  <div class="header">
    <h2>ZAPYS - Painel</h2>
  </div>
  <div class="logo"><img src="/logoPAGE.png" alt=""></div>
  <div class="container">
    <select v-model="selectedEndpoint">
      <option value="escolha" style="display: none;" disabled hidden>Escolha:</option>
      <option value="nome">Nome - V1</option>
      <option value="placa">Placa - V1</option>
      <option value="cpf">CPF - V1</option>
      <option value="cpfv2">CPF - V2</option>
      <option value="cep">CEP - V1 (lento)</option>
      <option value="foto">Foto - V1</option>
      <option value="email">Email - V1 </option>

    </select>

    <div class="components">
      <input type="text" v-model="token" placeholder="Token: ">
      <input type="text" v-model="dado" placeholder="Insira aqui: ">
      <button @click="requestData">Enviar</button>
    </div>

    <div class="response-data" v-if="responseData">
      <div v-if="selectedEndpoint === 'cep'">
        <p>CEP: {{ responseData.cep }}</p>
        <p>LOGRADOURO: {{ responseData.logradouro }}</p>
        <p>COMPLEMENTO: {{ responseData.complemento }}</p>
        <p>BAIRRO: {{ responseData.bairro }}</p>
        <p>LOCALIDADE: {{ responseData.localidade }}</p>
        <p>UF: {{ responseData.uf }}</p>
        <p>IBGE: {{ responseData.ibge }}</p>
        <p>GIA: {{ responseData.gia }}</p>
        <p>DDD: {{ responseData.ddd }}</p>
        <p>SIAFI: {{ responseData.siafi }}</p>
      </div>
      
      <div v-else-if="selectedEndpoint === 'nome'">
        <div v-for="(data, index) in responseData" :key="index">
          <p v-for="(value, key) in data" :key="key">{{ key.toUpperCase() }}: {{ value }}</p>
        </div>
      </div>
      <div v-else-if="selectedEndpoint === 'cpfv2'">
        <p>CPF: {{ responseData.cpf }}</p>
        <p>Nome do Pai: {{ responseData.pai }}</p>
        <p>Nome da Mãe: {{ responseData.mae }}</p>
        <p>CPF: {{ responseData.cpf }}</p>
        <p>Nome do Pai: {{ responseData.pai }}</p>
        <p>Nome da Mãe: {{ responseData.mae }}</p>
        <p>Município de Nascimento: {{ responseData.municipioNascimento }}</p>
        <p>Município: {{ responseData.municipio }}</p>
        <p>Logradouro: {{ responseData.logradouro }}</p>
        <p>Número: {{ responseData.numero }}</p>
        <p>Bairro: {{ responseData.bairro }}</p>
        <p>CEP: {{ responseData.cep }}</p>
        <p>RG Número: {{ responseData.rgNumero }}</p>
        <p>RG Órgão Emissor: {{ responseData.rgOrgaoEmissor }}</p>
        <p>RG UF: {{ responseData.rgUf }}</p>
        <p>RG Data de Emissão: {{ responseData.rgDataEmissao }}</p>
        <p>CNS: {{ responseData.cns }}</p>
        <p>Telefone: {{ responseData.telefone }}</p>
        <p>Telefone Secundário: {{ responseData.telefoneSecundario }}</p>
      </div>
      <div class="response-data" v-else-if="selectedEndpoint === 'placa'">
        <p>ID: {{ responseData.id }}</p>
        <p>Data Atualização: {{ responseData.data_atualizacao }}</p>
        <p>Chassi: {{ responseData.chassi }}</p>
        <p>Placa: {{ responseData.placa }}</p>
        <p>Faturado: {{ responseData.faturado }}</p>
        <p>Ano de Fabricação: {{ responseData.ano_fabricacao }}</p>
        <p>Município: {{ responseData.municipio }}</p>
        <p>UF da Placa: {{ responseData.uf_placa }}</p>
        <p>Marca e Modelo: {{ responseData.marca_modelo }}</p>
        <p>Combustível: {{ responseData.combustivel }}</p>
        <p>Potência: {{ responseData.potencia }}</p>
        <p>Capacidade de Carga: {{ responseData.capacidade_carga }}</p>
        <p>Nacionalidade: {{ responseData.nacionalidade }}</p>
        <p>Linha: {{ responseData.linha }}</p>
        <p>Carroceria: {{ responseData.carroceria }}</p>
        <p>Caixa de Câmbio: {{ responseData.caixa_cambio }}</p>
        <p>Eixo Traseiro Diferencial: {{ responseData.eixo_traseiro_dif }}</p>
        <p>Terceiro Eixo: {{ responseData.terceiro_eixo }}</p>
        <p>Motor: {{ responseData.motor }}</p>
        <p>Tipo de Documento do Faturado: {{ responseData.tipo_doc_faturado }}</p>
        <p>UF do Faturado: {{ responseData.uf_faturado }}</p>
        <p>Tipo de Documento do Proprietário: {{ responseData.tipo_doc_prop }}</p>
        <p>Ano do Modelo: {{ responseData.ano_modelo }}</p>
        <p>Tipo de Veículo: {{ responseData.tipo_veiculo }}</p>
        <p>Espécie do Veículo: {{ responseData.especie_veiculo }}</p>
        <p>Tipo de Carroceria: {{ responseData.tipo_carroceria }}</p>
        <p>Cor do Veículo: {{ responseData.cor_veiculo }}</p>
        <p>Quantidade de Passageiros: {{ responseData.quantidade_passageiro }}</p>
        <p>Situação do Chassi: {{ responseData.situacao_chassi }}</p>
        <p>Eixos: {{ responseData.eixos }}</p>
        <p>Tipo de Montagem: {{ responseData.tipo_montagem }}</p>
        <p>Tipo de Documento da Importadora: {{ responseData.tipo_doc_importadora }}</p>
        <p>Identificação da Importadora: {{ responseData.ident_importadora }}</p>
        <p>DI: {{ responseData.di }}</p>
        <p>Registro DI: {{ responseData.registro_di }}</p>
        <p>Unidade Local SRF: {{ responseData.unidade_local_srf }}</p>
        <p>Última Atualização: {{ responseData.ultima_atualizacao }}</p>
        <p>Restrição 1: {{ responseData.restricao_1 }}</p>
        <p>Restrição 2: {{ responseData.restricao_2 }}</p>
        <p>Restrição 3: {{ responseData.restricao_3 }}</p>
        <p>Restrição 4: {{ responseData.restricao_4 }}</p>
        <p>Limite Restrição Tributária: {{ responseData.limite_restricao_trib }}</p>
        <p>Cilindradas: {{ responseData.cilindradas }}</p>
        <p>Capacidade Máxima de Tração: {{ responseData.cap_maxima_tracao }}</p>
        <p>Peso Bruto Total: {{ responseData.peso_bruto_total }}</p>
        <p>Situação do Veículo: {{ responseData.situacao_veiculo }}</p>
        <p>Placa Modelo Antigo: {{ responseData.placa_modelo_antigo }}</p>
        <p>Placa Modelo Novo: {{ responseData.placa_modelo_novo }}</p>
        <p>Placa Nova: {{ responseData.placa_nova }}</p>
      </div>
      <div class="response-data" v-else>
        <p style="font-weight: bold;">EM BREVE</p>
      </div>
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
  computed: {
    formattedData() {
      if (this.responseData) {
        return JSON.stringify(this.responseData, null, 2);
      }
      return '';
    }
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
          maxRedirects: 0,
          validateStatus: function (status) {
            return status >= 200 && status < 400;
          },
        });
        this.responseData = response.data;
      } catch (error) {
        this.responseData = "não encontrado";
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

.components {
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

.header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: rgba(255, 255, 0, 0.849);
  color: black;
  text-align: center;
  z-index: 999;
}

.container {
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

select section .escolha {
  display: none;
}

select::-ms-expand {
  display: none;
}

select:hover {
  border-color: yellow;
}

select:focus {
  border-color: yellow;
}

.response-data {
  margin-top: 20px;
  padding: 10px;
  background-color: #1a1a1a;
  color: yellow;
  border-radius: 8px;
  max-height: 300px;
  /* Tamanho máximo da div */
  overflow-y: auto;
  /* Adicionar barra de rolagem vertical quando necessário */
}

img {
  max-height: 130px;
  max-width: 130px;
}
</style>
