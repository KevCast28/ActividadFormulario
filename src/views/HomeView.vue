<script setup lang="ts">
import { ref } from 'vue';
import type { Ref } from 'vue';
  const name:Ref<string> = ref('');
  const lastName:Ref<string> = ref('');
  const age:Ref<number> = ref(0);
  const sex:Ref<string[]> = ref(['Masculino', 'Femenino', 'Otro']);
  const selectedSex:Ref<string> = ref('');

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

function validateSex() {
  if (selectedSex.value === 'Otro') {
    sexError = 'Por favor, especifica el género';
  } else {
    sexError = '';
  }
}

function submitForm() {
  if (!hasErrors) {
    // Aquí puedes enviar el formulario si no hay errores
    console.log('Formulario enviado correctamente');
  }
}

function hasErrors() {
  return nameError || lastNameError || ageError || sexError;
}

</script>

<template>
  <div>
    <input v-model="name" type="text" @input="validateName">
    <span v-if="nameError" class="error">{{ nameError }}</span>
  </div>
  <div>
    <input v-model="lastName" type="text" @input="validateLastName">
    <span v-if="lastNameError" class="error">{{ lastNameError }}</span>
  </div>
  <div>
    <input v-model="age" type="number" @input="validateAge">
    <span v-if="ageError" class="error">{{ ageError }}</span>
  </div>
  <div>
    <select v-model="selectedSex" @change="validateSex">
      <option value="Masculino">Masculino</option>
      <option value="Femenino">Femenino</option>
      <option value="Otro">Otro</option>
    </select>
    <span v-if="sexError" class="error">{{ sexError }}</span>
  </div>
  <div>
    <button @click="submitForm" :disabled="hasErrors('')">Enviar</button>
  </div>
</template>

<style scoped>
  /* Estilos para los contenedores de los campos */
  div {
    margin-bottom: 10px;
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
