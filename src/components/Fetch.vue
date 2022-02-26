<script setup>
import { ref } from 'vue';

const data = ref('');

const fetchRandomUser = () => {
  console.log('fetch random user');
  fetch('https://randomuser.me/api/')
    .then((stream) => stream.json())
    .then((randomUsers) => (data.value = randomUsers))
    .catch((error) => console.error(error));
};

const fetchRandomUserAsync = async () => {
  console.log('fetch random user async');

  const response = await fetch('https://randomuser.me/api/');

  if (!response.ok) {
    console.log(`An error has occured: ${response.status}`);
    // throw new Error();
  }

  data.value = await response.json();
};

// fetchRandomUser();
await fetchRandomUserAsync();
</script>

<template>
  <div>Komponente mit Fetch API</div>
  <div>Daten: {{ data }}</div>
</template>
