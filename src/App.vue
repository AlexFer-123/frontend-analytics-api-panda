<template>
  <div class="bg bg-dark bg-gradient py-4 d-flex">
    <div class="container">
      <div class="row">
        <div class="col-12 pb-4">
          <h1 class="text-white">Gerador de dados do analytics</h1>
        </div>
        <div class="col-12 col-lg-6">
          <form class="text-white">
            <div class="form-group pb-4">
              <label for="exampleInputEmail1">Ensira sua API key</label>
              <input 
                v-model="dataRequest.api_key" 
                type="text" 
                class="form-control" 
                id="exampleInputEmail1" 
                aria-describedby="emailHelp" 
                placeholder="Ensira sua API key">
            </div>
            <div class="form-group pb-4">
              <label for="inputState">State</label>
              <select v-model="selectedType" id="inputState" class="form-control">
                <option v-for="type in types" :key="type">{{ type.name }}</option>
              </select>
            </div>
            <div class="form-group pb-4">
              <label for="exampleInputPassword1">Data de ínicio:</label>
              <input 
                v-model="dataRequest.start_date" 
                class="form-control" 
                v-mask="'####-##-##'"
                placeholder="yyyy-mm-dd"
              >
            </div>
            <div class="form-group pb-4">
              <label for="exampleInputPassword1">Data de fim:</label>
              <input 
                v-model="dataRequest.start_date" 
                class="form-control" 
                placeholder="yyyy-mm-dd" 
                v-mask="'####-##-##'"
              >
            </div>
            <button @click.prevent="request()" type="submit" class="btn btn-primary">Buscar</button>
          </form>
        </div>
        <div class="col-12 col-lg-6">oi</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue"
import http from './services/http'

const dataRequest = ref({
  start_date: '2023-12-01',
  end_date: '2023-12-31',
  api_key: 'panda-ee764cc77fd0825d8005de3e82848fef259a03047c2d2d42b25fda0f9780d3fb'
})

const selectedType = ref()
const analyticsData = ref([])
const types = [
  {
    name: "Dados Gerais",
  },
  {
    name: "Dados por vídeo",
  }
]

const request = async () => {
  
  if(selectedType.value === 'Dados Gerais') {
    const data = await http.post('/analytics', dataRequest.value)
    analyticsData.value.push(data)
  } else {
    const data = await http.post('/', dataRequest.value)
    analyticsData.value.push(data)
  }

  console.log(analyticsData.value)

}


</script>

<style>
  .bg {
    height: 100dvh;
  }
</style>
