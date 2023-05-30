<template>
  <div class="splashscreen">
    <img src="@/assets/logo-icon.svg" alt="Logo">
    <h1><span>Cash</span>Flow</h1>
  </div>
</template>

<script setup>
</script>
<style scoped>
.splashscreen {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

h1 {
  color: var(--brand-blue);
}

h1 span {
  color: var(--brand-green);
}
</style>