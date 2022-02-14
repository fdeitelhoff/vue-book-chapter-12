<script setup>
import { reactive } from 'vue';
import axios from 'axios';

// axios
//   .get('https://randomuser.me/api/')
//   .then(function (response) {
//     console.log(response.data.results);
//   })
//   .catch(function (error) {
//     console.log(error);
//   })
//   .then(function () {
//     console.log('Get Request');
//   });
const data = reactive({});

try {
  // const response = await axios.get('https://randomuser.me/api/');
  const response = await axios.get('https://randomuser.me/api/', {
    params: { results: 500 },
  });
  data.value = response.data.results;

  console.log('response', response.data.results);
} catch (error) {
  console.log('error', error);
}
</script>

<template>
  <div>
    <!-- {{ data }} -->
  </div>
</template>
