<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <Resume :label="label" :totalLabel="'Ahorro total'" :totalAmount="99999999" :amount="100000">
        <template #graphic>Gráficos</template>
        <template #action>Acciones</template>
      </Resume>
    </template>
    <template #movements>
      <Movements :movements="movements" />
    </template>
  </Layout>
</template>

<script setup>
import Header from '@/commons/Header.vue';
import Layout from '@/commons/Layout.vue';
import Movements from '@/commons/Movements.vue';
import Resume from '@/commons/Resume.vue';

const label = 'Label'

const movements = [
  { id: 1, title: "Movimiento", description: "Deposito de salario", amount: 1000 },
  { id: 2, title: "Movimiento 1", description: "Deposito de honorarios", amount: 500 },
  { id: 3, title: "Movimiento 3", description: "Comida", amount: -100 },
  { id: 4, title: "Movimiento 4", description: "Colegiatura", amount: 1000 },
  { id: 5, title: "Movimiento 5", description: "Reparación equipo", amount: 1000 },
]

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
