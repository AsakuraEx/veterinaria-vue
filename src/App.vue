<script setup>
  import Header from './components/Header.vue';
  import Formulario from './components/Formulario.vue'
  import { ref, reactive } from 'vue';

  const pacientes = ref([]);

  const paciente = reactive({
        nombre: '',
        propietario: '',
        email: '',
        alta: '',
        sintomas: ''
    });

    const guardarPaciente = () => {
        pacientes.value.push(paciente);
    }

</script>

<template>
  <div class="container mx-auto mt-20">
    
    <Header />

    <div class="mt-12 md:flex">
      
      <Formulario 
        v-model:nombre="paciente.nombre"
        v-model:propietario="paciente.propietario"
        v-model:email="paciente.email"
        v-model:alta="paciente.alta"
        v-model:sintomas="paciente.sintomas"
        @guardar-paciente="guardarPaciente"
      />

      <div
        class="md:w-1/2 text-center font-black text-3xl"
      >
        <h3>Administra los pacientes</h3>

        <div
          v-if="pacientes.length > 0"
          class=""
        >

        </div>
        <p
          v-else 
          class="font-normal text-2xl mt-20"
        >
            No hay pacientes

        </p>

      </div>
    
    </div>

  </div>

</template>

