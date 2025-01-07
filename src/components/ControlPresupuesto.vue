<script setup>
import { computed } from 'vue'
import CircleProgress from 'vue3-circle-progress'
import "vue3-circle-progress/dist/circle-progress.css"
import { formatearCantidad } from '../helpers'

const props = defineProps({
    presupuesto: {
        type: Number,
        required: true
    },
    disponible: {
        type: Number,
        requiered: true
    },
    gastado: {
        type: Number,
        required: true
    }
})
    defineEmits(['reset-app'])

    const porcentaje = computed(() => {
        return parseInt(((props.presupuesto - props.disponible) / props.presupuesto) * 100)
    })

</script>


<template>
    <div class="dos-columnas">

        <div class="contenedor-grafico">
            
            <p class="porcentaje">{{ porcentaje }}%</p>
            
            <CircleProgress
                :percent="porcentaje"
                :size="250"
                :border-width="30"
                :border-bg-width="30"
                fill-color="#3b82f6"
                empty-color="#e1e1e1"
            />
        </div>

        <div class="contenedor-presupuesto">
            <button 
                class="reset-app"
                type="button"
                @click="$emit('reset-app')"    
            >
                Resetear App
            </button>

            <p>
                <span>Presupuesto:</span>
                {{ formatearCantidad(presupuesto) }}
            </p>
            <p>
                <span>Disponible:</span>
                {{ formatearCantidad(disponible) }}
            </p>
            <p>
                <span>Gastado:</span>
                {{ formatearCantidad(gastado) }}
            </p>
        </div>

    </div>
</template>


<style scoped>

    .contenedor-grafico {
        position: relative;
    }

    .porcentaje {
        position: absolute;
        margin: auto;
        top: calc(50% - 3.5rem);
        text-align: center;
        right: 0;
        left: 0;
        z-index: 1;
        font-size: 6rem;
        font-weight: 900;
        color: var(--gris-oscuro);
    }

    .dos-columnas {
        display: flex;
        flex-direction: column;
    }

    .dos-columnas> :first-child {
        margin-bottom: 3rem;
    }


    .contenedor-presupuesto {
        width: 100%;
    }

    .contenedor-presupuesto p {
        font-size: 2.4rem;
        text-align: center;
        color: var(--gris-oscuro);
    }

    .contenedor-presupuesto span {
        font-weight: 900;
        color: var(--azul);
    }

    .reset-app {
        background-color: #db2777;
        border: none;
        padding: 1rem;
        width: 100%;
        color: var(--blanco);
        font-weight: 900;
        text-transform: uppercase;
        border-radius: 1rem;
        transition: background-color 300ms ease;
    }

    .reset-app:hover {
        cursor: pointer;
        background-color: #c11d67;
    }


    @media (min-width: 768px) {
        .dos-columnas {
            flex-direction: row;
            gap: 4rem;
            align-items: center;
        }

        .dos-columnas> :first-child {
            margin-bottom: 0;
        }

        .contenedor-presupuesto p {
        text-align: left;
        }
    }
</style>