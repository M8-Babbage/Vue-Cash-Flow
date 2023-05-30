<template>
  <!-- Suspense nos permite cargar el componente antes de la carga asincrona -->
  <Suspense>
    <!-- Slot de carga de componente por defecto -->
    <template #default>
      <Home />
    </template>
    <!-- Slot de carga de componente antes de la carga -->
    <template #fallback>
      <SplashScreen />
    </template>
  </Suspense>
</template>
<script setup>
import { defineAsyncComponent } from 'vue';
import SplashScreen from './commons/SplashScreen.vue';

// Importamos la vista Home simulando una carga lenta con un setTimeout de 2 segundos, para que se vea el SplashScreen.
const Home = defineAsyncComponent(() => new Promise((resolve) => {
  setTimeout(() => {
    resolve(import('./views/HomeView.vue'));
  }, 2000);
}));

</script>
<style>
html,
body,
.app {
  min-height: 100vh;
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
}

* {
  --brand-green: #04b500;
  --brand-blue: #0689b0;
}
</style>