<template>
  <div class="flex flex-col gap-8 divide-y divide-gray-100">
    <div>
      <h2 class="text-3xl font-extrabold text-gray-900">Recent articles</h2>
      <p class="mt-3 text-lg text-gray-400 mt-2">
        Discover articles from Nuxt team.
      </p>
    </div>

    <!-- TODO: List of `Article` -->
    <div>
      <ul v-for="article in articles">
        <li>{{article}}</li>
      </ul>
    </div>
    <!--end todo-->
  </div>
</template>

<script setup>
const { data: articles } = await useAsyncData('articles', () => {
  // TODO: Fetch articles from `content/` ordered by date DESC
  // https://content.nuxtjs.org/api/composables/query-content#find
  const articless = queryContent('content').find()
  // end todo
  return [articless];
});
</script>
