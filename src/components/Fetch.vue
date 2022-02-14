<script setup>
const storeItemUrl = '';

const fetchStoreItems = () => {
  console.log('fetch store items');
  fetch(storeItemUrl)
    .then((stream) => stream.json())
    .then((data) => (this.items = data))
    .catch((error) => console.error(error));
};

const fetchStoreItemsAsync = async () => {
  console.log('fetch store items async');

  const response = await fetch(storeItemUrl);

  if (!response.ok) {
    console.log(`An error has occured: ${response.status}`);
    // throw new Error();
  }

  const data = await response.json();
};

// fetchStoreItems();
// await fetchStoreItemsAsync();
</script>

<template>
  <div>Komponente mit Fetch API</div>
</template>
