<script setup>
    import { ref, computed } from 'vue'
    import Alerta from './Alerta.vue'
    import cerrarModal from '../assets/img/cerrar.svg'

    const error = ref('')

    const emit = defineEmits(['ocultar-modal', 'guardar-gasto', 'update:nombre', 'update:cantidad', 'update:categoria', 'eliminar-gasto'])

    const props = defineProps({
        modal: {
            type: Object,
            required: true
        },
        nombre: {
            type: String,
            required: true
        },
        cantidad: {
            type: [String, Number],
            required: true
        },
        categoria: {
            type: String,
            required: true
        },
        disponible: {
            type: Number,
            required: true
        },
        id: {
            type: [String, null],
            required: true
        }
    })

    const old = props.cantidad

    const agregarGasto = () => {
        // Validar que no haya campos vacíos
        const { cantidad, categoria, nombre, disponible, id } = props
        if ([nombre, cantidad, categoria].includes('')) {
            error.value = 'Todos los campos son obligatorios'
            setTimeout(() => {
               erro.value = '' 
            }, 2500);
            return
        }

        // Validad cantidad
        if(cantidad <= 0) {
            error.value = 'Cantidad no valida'
            setTimeout(() => {
               erro.value = '' 
            }, 2500);
            return
        }

        // Validar qe el usuario no gaste más de lo disponible
        if(id) {
            // Tomar en cuenta el hasto ya realizado
            if(cantidad > old + disponible) {
                error.value = 'Has excedido el presupuesto'
                setTimeout(() => {
                    error.value = '' 
                }, 2500);
                return
            }
        } else {
            if(cantidad > disponible) {
                error.value = 'Has excedido el presupuesto'
                setTimeout(() => {
                    error.value = '' 
                }, 2500);
                return
            }
        }


        emit('guardar-gasto')
    };

    const isEditing = computed(() => {
        return props.id
    })
</script>


<template>
    <div class="modal">
        <div class="cerrar-modal">
            <img 
                :src="cerrarModal" 
                alt="icono cerrar modal"
                @click="$emit('ocultar-modal')"
            />
        </div>

        <div class="contenedor contenedor-formulario"
            :class="[modal.animar ? 'animar' : 'cerrar']"
        >
            <form 
                class="nuevo-gasto"
                @submit.prevent="agregarGasto"
            >

                <legend>{{ isEditing === null ? 'Añadir Gasto' : 'Editar Gasto' }}</legend>


                <Alerta v-if="error">{{ error }}</Alerta>

                <div class="campo">
                    <label for="nombre">Nombre Gasto:</label>
                    <input 
                        id="nombre" 
                        type="text"
                        placeholder="Añade el Nombre del Gasto"
                        :value="nombre"
                        @input="$emit('update:nombre', $event.target.value)"
                    >
                </div>
                
                <div class="campo">
                    <label for="cantidad">Cantidad:</label>
                    <input 
                        id="cantidad" 
                        type="number"
                        placeholder="Añade la Cantidad del Gasto"
                        :value="cantidad"
                        @input="$emit('update:cantidad', +$event.target.value)"
                    >
                </div>

                <div class="campo">
                    <label for="categoria">Categoría:</label>
                    <select 
                        name="categoria" 
                        id="categoria"
                        :value="categoria"
                        @input="$emit('update:categoria', $event.target.value)"
                    >
                        <option value="">-- Seleccione --</option>
                        <option value="ahorro">Ahorro</option>
                        <option value="comida">Comida</option>
                        <option value="casa">Casa</option>
                        <option value="gastos">Gastos Varios</option>
                        <option value="ocio">Ocio</option>
                        <option value="salud">Salud</option>
                        <option value="suscripciones">Suscripciones</option>
                    </select>
                </div>

                <input type="submit" :value="[isEditing ? 'Guardar Cambios' : 'Añadir Gasto']">
            </form>

            <button
             class="btn-eliminar"
             type="button"
             v-if="isEditing"
             @click="$emit('eliminar-gasto', id)"
            >
                Eliminar Gasto
            </button>
        </div>
    </div>
</template>


<style scoped>

    .modal {
        position: absolute;
        background-color: rgb(0 0 0 / 0.9);
        top: 0;
        bottom: 0;
        right: 0;
        left: 0;
    }

    .cerrar-modal {
    position: absolute;
    top: 5rem;
    right: 5rem;
  }

  .cerrar-modal img {
    width: 5rem;
    cursor: pointer;
    transition: scale 300ms ease;
  }

  .cerrar-modal img:hover {
    scale: 1.1;
  }

  .contenedor-formulario {
    transition: all 300ms ease-in;
    opacity: 0;
  }

  .contenedor-formulario.animar {
    opacity: 1;
  }

  .contenedor-formulario.cerrar {
    opacity: 0;
  }

  .nuevo-gasto {
    margin: 10rem auto 0 auto;
    display: grid;
    gap: 2rem;
  }

  legend {
    text-align: center;
    color: var(--blanco);
    font-size: 3rem;
    font-weight: 700;
  }

  .campo {
    display: grid;
    gap: 2rem;
  }

  .nuevo-gasto input,
  .nuevo-gasto select {
    background-color: var(--gris-claro);
    border-radius: 1rem;
    padding: 1rem;
    border: none;
    font-size: 2.2rem;
  }

  .nuevo-gasto label {
    color: var(--blanco);
    font-size: 3rem;
  }

  .nuevo-gasto input[type="submit"] {
    background-color: var(--azul);
    color: var(--blanco);
    font-weight: 700;
    cursor: pointer;
  }

  .btn-eliminar {
    padding: 1rem;
    width: 100%;
    background-color: #ef4444;
    font-size: 1.2rem;
    font-weight: 700;
    color: var(--blanco);
    margin-top: 10rem;
    cursor: pointer;
    border: none;
  }


</style>