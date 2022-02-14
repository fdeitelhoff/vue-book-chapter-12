<script setup>
import Fetch from './components/Fetch.vue';
import Axios from './components/Axios.vue';
import AxiosPagination from './components/AxiosPagination.vue';
</script>

<template>
  <Fetch />
  <suspense>
    <template #default>
      <Axios />
    </template>
    <template #fallback>
      <div>Daten werden geladen...</div>
    </template>
  </suspense>
  <suspense>
    <template #default>
      <AxiosPagination />
    </template>
    <template #fallback>
      <div>Daten werden geladen...</div>
    </template>
  </suspense>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
