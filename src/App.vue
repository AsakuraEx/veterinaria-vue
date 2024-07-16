<script setup>

  import { ref, reactive } from 'vue';
  import { uid } from 'uid'

  import Header from './components/Header.vue';
  import Formulario from './components/Formulario.vue'
  import Paciente from './components/Paciente.vue'


  const pacientes = ref([]);

  const paciente = reactive({
        id: uid(),
        nombre: '',
        propietario: '',
        email: '',
        alta: '',
        sintomas: ''
    });

    const guardarPaciente = () => {
        pacientes.value.push({
          ...paciente //genera una copia
        });

        Object.assign(paciente, {
          id: uid(),
          nombre: '',
          propietario: '',
          email: '',
          alta: '',
          sintomas: ''
        })
    }

    const actualizarPaciente = (id) => {
      const pacienteEditar = pacientes.value.filter(paciente => paciente.id === id)[0]; //Busca el paciente que coincida con el id evaluado en filter, devuelve un nuevo array
      Object.assign(paciente,pacienteEditar); //se asigna al paciente reactivo los valores del pacienteEditar
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

      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra los pacientes</h3>
        <p class="text-lg mt-5 text-center mb-10">
          Información de
          <span class="text-indigo-600 font-bold">Pacientes</span>
        </p>
        <div v-if="pacientes.length > 0">
          
          <Paciente 
            v-for="paciente in pacientes"
            :paciente="paciente"
            @actualizar-paciente="actualizarPaciente"
          />

        </div>
        <p v-else class="text-2xl mt-20 text-center">
            No hay pacientes
        </p>

      </div>
    
    </div>

  </div>

</template>

