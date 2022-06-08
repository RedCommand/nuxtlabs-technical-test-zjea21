<template>
  <!-- TODO: Render markdown from fetched article -->
  <!-- https://content.nuxtjs.org/guide/displaying/rendering -->
  <div class="prose max-w-none" />
</template>

<script setup>
const route = useRoute();

const { data } = await useAsyncData(route.path, () => {
  // TODO: Fetch article from `content/`
  // https://content.nuxtjs.org/api/composables/query-content#findone
  return [];
});
</script>
