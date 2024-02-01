<script setup lang="ts">
import { ref } from 'vue';
import type { Ref } from 'vue';
  const name:Ref<string> = ref('');
  const lastName:Ref<string> = ref('');
  const age:Ref<number> = ref(0);
  const sex:Ref<string[]> = ref(['Masculino', 'Femenino', 'Otro']);
  const selectedSex:Ref<string> = ref('');
  const customGender:Ref<string> = ref('');

  let nameError = '';
  let lastNameError = '';
  let ageError = '';
  let sexError = '';

  function validateName() {
  if (name.value.length < 5 || name.value.length > 18) {
    nameError = 'El nombre debe tener entre 5 y 18 caracteres';
  } else {
    nameError = '';
  }
}

function validateLastName() {
  if (lastName.value === name.value) {
    lastNameError = 'El apellido no puede ser igual al nombre';
  } else {
    lastNameError = '';
  }
}

function validateAge() {
  if (age.value <= 0 || age.value >= 60) {
    ageError = 'La edad debe ser mayor que 0 y menor que 60';
  } else {
    ageError = '';
  }
}

function handleSexChange() {
  sexError = '';
}

function submitForm() {
  if (!hasErrors) {
    // Aquí puedes enviar el formulario si no hay errores
    console.log('Formulario enviado correctamente');
  }
}

function hasErrors(): boolean {
    return !!nameError || !!lastNameError || !!ageError || !!sexError;
}

</script>

<template>
  <div class="form-container">
    <h1>Formulario</h1>
    <div class="form-field">
    <label for="name">Nombre</label>
    <input id="name" v-model="name" type="text" @input="validateName">
    <span v-if="nameError" class="error">{{ nameError }}</span>
  </div>
  <div>
    <label for="name">Apellido</label>
    <input id="last-name" v-model="lastName" type="text" @input="validateLastName">
    <span v-if="lastNameError" class="error">{{ lastNameError }}</span>
  </div>
  <div>
    <label for="name">Edad</label>
    <input id="age" v-model="age" type="number" @input="validateAge">
    <span v-if="ageError" class="error">{{ ageError }}</span>
  </div>
  <div>
    <label for="name">Género</label>
    <select id="sex" v-model="selectedSex" @change="handleSexChange">
      <option value="Masculino">Masculino</option>
      <option value="Femenino">Femenino</option>
      <option value="Otro">Otro</option>
    </select>
    <span v-if="sexError" class="error">{{ sexError }}</span>
  </div>
  <div v-if="selectedSex === 'Otro'" class="form-field">
      <label for="custom-gender">Especificar género</label>
      <input id="custom-gender" v-model="customGender" type="text">
    </div>
  <div>
    <button @click="submitForm" :disabled="hasErrors()">Enviar</button>
  </div>
  </div>
</template>

<style scoped>
  /* Estilos para los contenedores de los campos */
  div {
    margin-bottom: 10px;
  }

  .form-container {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
}

.form-field {
  margin-bottom: 15px;
}

label {
  font-weight: bold;
  margin-right: 10px;
}

  /* Estilos para los campos de entrada */
  input[type="text"],
  input[type="number"],
  select {
    width: 100%;
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
    font-size: 16px;
  }

  /* Estilos para el botón */
  button {
    background-color: #4CAF50;
    color: white;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }

  button:hover {
    background-color: #45a049;
  }

  .error {
  color: red;
  }
</style>
