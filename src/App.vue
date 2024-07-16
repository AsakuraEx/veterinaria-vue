<script setup>

  import { ref, reactive, watch, onMounted } from 'vue';
  import { uid } from 'uid'

  import Header from './components/Header.vue';
  import Formulario from './components/Formulario.vue'
  import Paciente from './components/Paciente.vue'

    onMounted(()=>{
      const pacientesStorage = localStorage.getItem('pacientes');
      if(pacientesStorage){
        pacientes.value = JSON.parse(pacientesStorage);
      }
    });

  const pacientes = ref([]);                      //Se define un array que contenga todos los pacientes reactivos

  const paciente = reactive({                     //Se define un objeto paciente reactivo
        id: null,
        nombre: '',
        propietario: '',
        email: '',
        alta: '',
        sintomas: ''
    });

    const guardarLocalStorage = () => {
      localStorage.setItem('pacientes', JSON.stringify(pacientes.value));
    }

    watch(pacientes, ()=>{
      guardarLocalStorage()
    },{
      deep: true
    });

    const guardarPaciente = () => {
        
      if(paciente.id){                            //Evalua si el paciente tiene un id, si no tiene id (null) es nuevo, sino es antiguo
        const { id } = paciente;                  //Se deconstruye el objeto y se genera una variable con el valor de paciente.id
        const i = pacientes.value.findIndex((pacienteState) => pacienteState.id === id);    //Se encuentra el index basado en la condicion
        pacientes.value[i] = {...paciente}      //Se guarda la copia del paciente en la posicion encontrada
      }else{                                        //Si es nuevo
        pacientes.value.push({                    //Guarda al final del arreglo una copia del paciente y asigna un id
          ...paciente,
          id: uid() //genera una copia
        });
      }


        Object.assign(paciente, {               //Se limpian los campos del formulario
          nombre: '',
          propietario: '',
          email: '',
          alta: '',
          sintomas: '',
          id: null
        })
    }

    const actualizarPaciente = (id) => {
      const pacienteEditar = pacientes.value.filter(pacienteState => pacienteState.id === id)[0]; //Busca el paciente que coincida con el id evaluado en filter, devuelve un nuevo array
      Object.assign(paciente,pacienteEditar); //se asigna al paciente reactivo los valores del pacienteEditar
    }

    const eliminarPaciente = (id) => {
      pacientes.value = pacientes.value.filter(pacienteState => pacienteState.id !== id);
    };




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
        :id="paciente.id"
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
            @eliminar-paciente="eliminarPaciente"
          />

        </div>
        <p v-else class="text-2xl mt-20 text-center">
            No hay pacientes
        </p>

      </div>
    
    </div>

  </div>

</template>

