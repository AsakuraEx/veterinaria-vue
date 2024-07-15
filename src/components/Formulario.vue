<script setup>

</script>

<template>

    <div class="md:w-1/2">
        <h2 class="font-black text-3xl text-center">Seguimiento Pacientes</h2>
        <p class="text-lg mt-5 text-center mb-10">
            Añade Pacientes y
            <span class="text-indigo-600 font-bold">Administralos</span>
        </p>

        <form
            class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
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
                />
            </div>
            <div class="mb-5">

                <input 
                    type="submit"
                    class="bg-indigo-600 text-white w-full py-3 font-bold uppercase hover:bg-indigo-800
                    cursor-pointer transition-colors"
                    value="Registrar Paciente"
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