<script setup>

    import { computed } from 'vue'

    const props = defineProps(
        {
            alerta: {
                type: Object,
                required:true
            }
        }
    );

    const isError = computed(function () {
        return props.alerta.tipo === 'error';
    });

</script>

<template>
    <div 
        :class="[isError ? 'bg-red-500': 'bg-green-500']"
        class="bg-red-500 p-3 uppercase mb-4 rounded-lg 
        text-center font-bold text-white shadow-md"
    >
        {{alerta.mensaje}}
    </div>
</template>