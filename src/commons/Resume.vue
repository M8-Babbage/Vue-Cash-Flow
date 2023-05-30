<template>
  <main>
    <p>{{ labelVisual }}</p>
    <h1>{{ amountCurrency }}</h1>
    <div class="graphic">
      <slot name="graphic"></slot>
    </div>
    <div class="action">
      <slot name="action"></slot>
    </div>
  </main>
</template>
<script setup>
import currencyFormater from "@/helpers/currency";
import { computed, toRefs } from "vue";

const props = defineProps(
  {
    label: {
      type: String,
      default: null,
    },
    totalLabel: {
      type: String,
      required: true
    },
    amount: {
      type: Number,
      default: null,
    },
    totalAmount: {
      type: Number,
      required: true
    }
  }
)

// Crear referencias reactivas a las propiedades
const { label, totalLabel, amount, totalAmount } = toRefs(props)

// Definir el label a mostrar
const labelVisual = computed(() => {
  return label.value !== null ? label.value : totalLabel.value;
})

// Formatear el monto a moneda local
const amountCurrency = computed(() => {
  const currency = amount.value !== null ? amount.value : totalAmount.value;
  return currencyFormater.format(currency)
})
</script>
<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}

h1,
p {
  margin: 0;
  text-align: center;
}

h1 {
  margin-top: 14px;
  color: var(--brand-green);
}

.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
}
</style>