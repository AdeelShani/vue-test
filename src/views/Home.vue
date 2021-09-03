<template>
  <h1>Hallo</h1>
  <div v-if="error">{{ error }}</div>
  <div v-for="artwork in artworks" :key="artwork.id">
    {{ artwork.label }}:

    {{ artwork.properties.Title }}
    <br />
    <br />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "Home",
  setup() {
    const artworks = ref([]);
    const error = ref(null);

    const loadData = async () => {
      try {
        const data = await fetch("https://localhost:5001/api/fineart");
        if (!data.ok) {
          throw Error("no data available");
        }
        artworks.value = await data.json();
      } catch (err) {
        error.value = err.message;
        console.log(error.value + " haha");
      }
    };

    loadData();

    return { artworks, error };
  },
});
</script>
