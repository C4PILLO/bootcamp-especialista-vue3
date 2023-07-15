<script setup>

import { ref } from "vue"

import empresas from './empresas.json' 

const DEAFULT_FORM_DATA = {
  id: null,
  name: ' ',
  owner: ' '
}

const enterprises = ref(empresas)

const formData = ref(DEAFULT_FORM_DATA)

const onSubmit = () => {

  const {id, name, owner} = formData.value

  const newId = crypto.randomUUID()
  const newEnterprise = {
    id: newId,
    name,
    owner
  }
  enterprises.value = [
    ...enterprises.value,
    newEnterprise
  ]

  console.log('guardando data...', newEnterprise);

}
 
</script>

<template>
  <div class="container">
    <nav>
      <ul>
        <li>Lista de empresas</li>
      </ul>
      <ul>
        <li>
          <button role="button">Nuevo company</button>
        </li>
      </ul>
    </nav>
    <div class="grid">
      <div>
        <table>
          <thead>
            <tr>
              <th>#</th>
              <th>Name</th>
              <th>Owner</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="empresa in enterprises" :key="empresa.id">
              <td>{{ empresa.id }}</td>
              <td>{{ empresa.name }}</td>
              <td>{{ empresa.owner }}</td>
            </tr>
          </tbody>
        </table>
      </div>
      <div>
        <!-- {{ formData }} -->
        <form @submit.prevent="onSubmit">
          <label>
            Nombre de la empresa
            <input 
            type="text"
            placeholder="Ex. Mi empresa"
            required
            v-model="formData.name"
            />
          </label>
          <label>
            Nombre propietario
            <input 
            type="text"
            placeholder="Ex. Capillo"
            required
            v-model="formData.owner"
            />
          </label>
          <button type="submit">
            Guardar
          </button>
        </form>
      </div>

    </div>


  </div>
</template>

<style scoped></style>
