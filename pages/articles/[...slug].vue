<template>
    <!-- TODO: Render markdown from fetched article -->
    <!-- https://content.nuxtjs.org/guide/displaying/rendering -->
    <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 pt-8 pb-16">
        <div class="prose max-w-none">
            <ContentDoc :value="data" />
        </div>
    </div>
</template>

<script setup>
const route = useRoute();

const { data } = await useAsyncData(route.path, () => {
    // TODO: Fetch article from `content/`
    // https://content.nuxtjs.org/api/composables/query-content#findone
    return new Promise((resolve) => {
        queryContent("articles")
            .where({ _path: route.path })
            .findOne()
            .then((articles) => resolve(articles));
    });
});
</script>
