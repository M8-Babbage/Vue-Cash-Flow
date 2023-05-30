<template>
  <Layout>
    <template #header>
      <Header />
    </template>
    <template #resume>
      <Resume />
    </template>
    <template #movements>
      <Movements />
    </template>
  </Layout>
</template>

<script setup>
import Header from '@/commons/Header.vue';
import Layout from '@/commons/Layout.vue';
import Movements from '@/commons/Movements.vue';
import Resume from '@/commons/Resume.vue';

</script>
<style scoped></style>
