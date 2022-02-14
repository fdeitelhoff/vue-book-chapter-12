<script setup>
import { ref, reactive, computed } from 'vue';
import axios from 'axios';

const data = reactive({});
const itemsPerPage = ref(2);
const currentPage = ref(1);
// const filter = ref('Artikel');
// const sort = ref('id');
// const sortOrder = ref('DESC');

const fetchData = async () => {
  try {
    const response = await axios.get('https://randomuser.me/api/', {
      params: {
        page: currentPage.value,
        results: itemsPerPage.value,
        seed: 'vue-3-buch',
      },
    });
    data.value = response.data.results;

    console.log('response', response.data.results);
  } catch (error) {
    console.log('error', error);
  }
};

// const sortAndFilter = computed(() => {
//   var localData;
//   if (filter.value !== '') {
//     localData = data.value.filter((item) =>
//       item.name.first.includes(filter.value)
//     );
//   }

//   if (sort !== '') {
//     localData = data.value.sort((a, b) => a < b);
//   }

//   if (sortOrder === 'DESC') {
//     localData.reverse();
//   }

//   return localData;
// });

const totalPages = ref(500);
const paginatedData = computed(() => {
  return data.value;
});

const setPage = async (pageNumber) => {
  if (pageNumber > totalPages) {
    currentPage.value = totalPages;
  } else if (pageNumber < 1) {
    pageNumber = 1;
  } else {
    currentPage.value = pageNumber;
  }

  console.log('set page', pageNumber);

  await fetchData();
};

await setPage(1);
</script>

<template>
  <div>
    <template v-for="pageNumber in totalPages">
      <span
        v-if="
          Math.abs(pageNumber - currentPage) < 3 ||
          pageNumber == totalPages ||
          pageNumber == 1
        "
        :key="pageNumber"
      >
        <a :key="pageNumber" href="#" @click="setPage(pageNumber)">
          {{ pageNumber }}</a
        ></span
      >
      &nbsp;
    </template>
    <ul>
      <li v-for="item in paginatedData" :key="item.id">{{ item.name }}</li>
    </ul>
  </div>
</template>
