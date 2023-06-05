<template>
  <div class="movement">
    <div class="content">
      <h4>{{ title }}</h4>
      <p>{{ description }}</p>
    </div>
    <div class="action">
      <img @click="remove" src="@/assets/trash-icon.svg" alt="Delete" />
      <p :class="amount > 0 ? 'green' : 'red'">{{ currencyAmount }}</p>
    </div>
  </div>
</template>
<script setup>
import currencyFormater from "@/helpers/currency";
import { computed, toRefs } from "vue";

// Definición de propiedades y emisiones
const props = defineProps({
  id: {
    type: Number,
    required: true,
  },
  title: {
    type: String,
    required: true,
  },
  description: {
    type: String,
    required: true
  },
  amount: {
    type: Number,
    required: true
  }
})

const emits = defineEmits(["onRemove"]);

// Crear referencias reactivas a las propiedades
const { id, title, description, amount } = toRefs(props)

// Formatear el monto a moneda local
const currencyAmount = computed(() => {
  return currencyFormater.format(amount.value);
})

// Emisión de evento para eliminar movimiento
const remove = () => {
  emits("onRemove", id.value);
};
</script>
<style scoped>
.movement {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  padding: 16px;
  background-color: #e6f9ff;
  border-radius: 8px;
  box-sizing: border-box;
}

.movement .content {
  width: 100%;
}

.movement .action {
  display: flex;
  justify-content: space-between;
  align-items: flex-end;
  flex-direction: column;
}

h4,
p {
  margin: 0;
  padding: 0;
}

h4 {
  margin-bottom: 8px;
}

.movement .action img {
  margin-bottom: 16px;
}

.red {
  color: red;
}

.green {
  color: green;
}

.action img {
  cursor: pointer;
}
</style>