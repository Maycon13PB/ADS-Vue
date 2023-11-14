<template>
    <div class="container">
      <h1>Consultar CEP</h1>
      <hr>
      <form action="#" @submit.prevent="getCep" class="form">
        <label for="cep">Digite o CEP:</label>
        <input type="text" id="cep" v-model="cep" class="input-field">
        <label for="format">Escolha o formato:</label>
        <select v-model="selectedFormat" id="format" class="input-field">
          <option value="json">JSON</option>
          <option value="xml">XML</option>
          <option value="csv">CSV</option>
        </select>
        <button type="submit" class="btn">Consultar</button>
      </form>
      <div class="result">
        <p>Rua: {{ place.street }}</p>
        <p>Bairro: {{ place.neighborhood }}</p>
        <p>Cidade: {{ place.city }}/{{ place.state }}</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import axios from 'axios'
  import { reactive, ref } from 'vue';
  
  const baseUrl = 'https://viacep.com.br/ws/'
  const format = reactive({
    json: '/json',
    xml: '/xml',
    csv: '/csv'
  })
  
  const cep = ref("")
  const selectedFormat = ref('json')
  
  const place = reactive({
    street: '',
    neighborhood: '',
    city: '',
    state: ''
  })
  
  const getCep = async () => {
    try {
      const response = await axios.get(baseUrl + cep.value + format[selectedFormat.value]);
      place.street = response.data.logradouro;
      place.neighborhood = response.data.bairro;
      place.city = response.data.localidade;
      place.state = response.data.uf;
    } catch (error) {
      console.error('Eita.. deu erro !', error)
    }
  }
  
  </script>
  
  <style scoped>
  .container {
    max-width: 500px;
    margin: 0 auto;
    padding: 20px;
    font-family: Arial, sans-serif;
  }
  
  .form {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
  }
  
  .input-field {
    padding: 8px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  .btn {
    padding: 8px 15px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  .result {
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 10px;
  }
  
  #format {
    margin-bottom: 10px;
  }
  </style>
  