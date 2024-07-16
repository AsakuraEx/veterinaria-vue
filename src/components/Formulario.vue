<script setup>
    import {reactive, computed} from 'vue';
    import Alerta from './Alerta.vue';

    const props = defineProps(
        {
            nombre:
            {
                type: String,
                required: true
            },

            propietario:
            {
                type: String,
                required: true
            },

            email:
            {
                type: String,
                required: true
            },

            alta:
            {
                type: String,
                required: true
            },

            sintomas:
            {
                type: String,
                required: true
            },
            id:
            {
                type: [String, null],
                required:true
            }
        }
    );

    const emit = defineEmits([
        'update:nombre', 'update:propietario', 'update:email',
        'update:alta', 'update:sintomas', 'guardar-paciente'
    ]);

    const alerta = reactive({
        tipo: '',
        mensaje: ''
    });

    const validar = (e) => {
      //  e.preventDefault(); Previene el evento de refresco de la pantalla (Javascript TOTAL perro uwu)
      if(Object.values(props).includes('')){ //includes evalua si al menos uno esta vacio
        alerta.mensaje = 'Todos los campos son obligatorios';
        alerta.tipo = 'error';
        return
      }
    
      emit('guardar-paciente');
      alerta.mensaje = 'Paciente Almacenado Correctamente';
      alerta.tipo = 'exito';

      setTimeout(() => {
        Object.assign(alerta, {
            tipo: '',
            mensaje: ''
        })
      }, 2000);

    }

    const editando = computed(() => {
        return props.id;
    });

</script>

<template>

    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>
        <p class="text-lg mt-5 text-center mb-10">
            Añade Pacientes y
            <span class="text-indigo-600 font-bold">Administralos</span>
        </p>

        <Alerta 
            v-if="alerta.mensaje"
            :alerta="alerta"
        />

        <form
            class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
            @submit.prevent="validar"
        >
            <div class="mb-5">

                <label 
                    for="mascota"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Nombre Mascota
                </label>

                <input 
                    type="text"
                    id="mascota"
                    placeholder="Nombre de la mascota"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    @input="$emit('update:nombre', $event.target.value)"
                    :value="nombre"
                >
            </div>

            <div class="mb-5">
                <label 
                    for="propietario"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Nombre Propietario
                </label>
                <input 
                    type="text"
                    id="propietario"
                    placeholder="Nombre del propietario"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    @input="$emit('update:propietario', $event.target.value)"
                    :value="propietario"
                >
            </div>
            <div class="mb-5">
                <label 
                    for="email"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Email
                </label>
                <input 
                    type="email"
                    id="email"
                    placeholder="Email del propietario"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    @input="$emit('update:email', $event.target.value)"
                    :value="email"
                >
            </div>
            <div class="mb-5">
                <label 
                    for="alta"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Alta
                </label>
                <input 
                    type="date"
                    id="alta"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md"
                    @input="$emit('update:alta', $event.target.value)"
                    :value="alta"
                >
            </div>
            <div class="mb-5">
                <label 
                    for="sintomas"
                    class="block text-gray-700 uppercase font-bold"
                >
                    Sintomas
                </label>
                <textarea 
                    placeholder="Escribe los sintomas"
                    id="sintomas"
                    class="border-2 w-full p-2 mt-2 placeholder-gray-400 rounded-md h-40"
                    @input="$emit('update:sintomas', $event.target.value)"
                    :value="sintomas"
                />
            </div>
            <div class="mb-5">

                <input 
                    type="submit"
                    class="bg-indigo-600 text-white w-full py-3 font-bold uppercase hover:bg-indigo-800
                    cursor-pointer transition-colors"
                    :value="[editando ? 'Guardar cambios':'Registrar Paciente']"
                >
                <input 
                    type="reset"
                    value="Limpiar formulario"
                    class="bg-gray-100 font-bold uppercase w-full py-3 mt-2 hover:bg-gray-300
                    cursor-pointer transition-colors"
                >
            </div>

        </form>
    </div>

</template>