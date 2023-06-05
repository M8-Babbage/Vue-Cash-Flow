<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <Resume :label="'Ahorro total'" :totalAmount="totalAmount" :amount="amount">
        <template #graphic>
          <Graphic :amounts="amounts" @select="select" />
        </template>
        <template #action>
          <Action @create="create" />
        </template>
      </Resume>
    </template>
    <template #movements>
      <Movements @onRemove="remove" :movements="movements" />
    </template>
  </Layout>
</template>

<script setup>
import Action from '@/commons/Action.vue';
import Header from '@/commons/Header.vue';
import Layout from '@/commons/Layout.vue';
import Movements from '@/commons/Movements.vue';
import Resume from '@/commons/Resume.vue';
import { computed, reactive, ref } from 'vue';
import Graphic from '../commons/Graphic.vue';

let amount = ref(0);

const movements = reactive([
  {
    id: 0,
    title: "Movimiento 1",
    description: "Lorem ipsum dolor sit amet",
    amount: 100,
    time: new Date("02-01-2022"),
  },
  {
    id: 1,
    title: "Movimiento 2",
    description: "Lorem ipsum dolor sit amet",
    amount: 200,
    time: new Date("02-01-2022"),
  },
  {
    id: 2,
    title: "Movimiento 3",
    description: "Lorem ipsum dolor sit amet",
    amount: 500,
    time: new Date("02-01-2022"),
  },
  {
    id: 3,
    title: "Movimiento 4",
    description: "Lorem ipsum dolor sit amet",
    amount: 200,
    time: new Date("02-01-2022"),
  },
  {
    id: 4,
    title: "Movimiento 5",
    description: "Lorem ipsum dolor sit amet",
    amount: -400,
    time: new Date("02-01-2022"),
  },
  {
    id: 5,
    title: "Movimiento 6",
    description: "Lorem ipsum dolor sit amet",
    amount: -600,
    time: new Date("02-01-2022"),
  },
  {
    id: 6,
    title: "Movimiento 7",
    description: "Lorem ipsum dolor sit amet",
    amount: -300,
    time: new Date("02-01-2022"),
  },
  {
    id: 7,
    title: "Movimiento 8",
    description: "Lorem ipsum dolor sit amet",
    amount: 100,
    time: new Date("02-01-2022"),
  },
  {
    id: 8,
    title: "Movimiento 9",
    description: "Lorem ipsum dolor sit amet",
    amount: 300,
    time: new Date("01-01-2022"),
  },
  {
    id: 9,
    title: "Movimiento 10",
    description: "Lorem ipsum dolor sit amet",
    amount: 500,
    time: new Date("01-01-2022"),
  },
])



const amounts = computed(() => {
  const lastDays = movements.filter(m => {
    const today = new Date();
    const oldDate = today.setDate(today.getDate() - 30);
    return m.time <= oldDate
  }).map(m => m.amount)

  return lastDays.map((m, i) => {
    const lastMovements = lastDays.slice(0, i + 1);
    return lastMovements.reduce((suma, movement) => {
      return suma + movement
    }, 0)
  })
})

const create = (movement) => {
  movement.id = movements.length;
  console.log(movement);
  movements.push(movement);
}

const remove = (id) => {
  const index = movements.findIndex(m => m.id === id);
  movements.splice(index, 1);
}

const totalAmount = computed(() => {
  return movements.reduce((suma, movement) => {
    return suma + movement.amount
  }, 0)
})

const select = (value) => {
  amount.value = value;
}

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
