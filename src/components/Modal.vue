<script setup>
    import cerrarModal from '../assets/img/cerrar.svg'

    const emit = defineEmits(['ocultar-modal'])
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

</style>