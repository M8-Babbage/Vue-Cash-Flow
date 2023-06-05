<template>
  <div class="movements">
    <h2 class="title">Historial</h2>
    <div class="content">
      <Movement v-for="{ id, title, description, amount } in movements" :key="id" :id="id" :title="title"
        :description="description" :amount="amount" @onRemove="onRemove(id)" />
    </div>
  </div>
</template>
<script setup>
import { toRefs } from 'vue';
import Movement from './Movement.vue';

const emits = defineEmits(['onRemove'])

const props = defineProps({
  movements: {
    type: Array,
    // Se debe retornar el arreglo dentro de una función porque si no, se compartiría la misma referencia entre todos los componentes que usen este componente
    default: () => [],
  },
})

// Generamos variables reactivas a partir de las props, cuidado con "toRef y toRefs"
const { movements } = toRefs(props)

// Escuchamos el evento "onRemove" con el id del movimiento a eliminar
const onRemove = (id) => {
  // Emitimos el evento "onRemove" con el id del movimiento a eliminar
  emits('onRemove', id)
}

</script>
<style scoped>
.movements {
  max-height: 100%;
  padding: 0 8px;
  margin-bottom: 14px;
}

.title {
  margin: 8px 16px 24px 16px;
  color: var(--brand-blue);
}

.content {
  max-height: 68vh;
  display: flex;
  flex-direction: column;
  gap: 8px;
  overflow-y: scroll;
}
</style>