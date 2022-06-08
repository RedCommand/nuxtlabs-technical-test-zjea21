<template>
    <div class="flex flex-col gap-8 divide-y divide-gray-100">
        <div>
            <h2 class="text-3xl font-extrabold text-gray-900">
                Recent articles
            </h2>
            <p class="mt-3 text-lg text-gray-400 mt-2">
                Discover articles from Nuxt team.
            </p>
            <div class="text-right">
			<input type="text" v-model="search" placeholder="Search titles..." />
                <button @click="sortDirection = !sortDirection">
                    <p v-if="sortDirection">Date ↑</p>
                    <p v-else>Date ↓</p>
                </button>
            </div>
        </div>
        <div class="text-center grid grid-cols-5 gap-4">
            <ul v-for="tag in tags" :key="tag">
                <button
                    @click="filterTag(tag)"
                    class="px-2 py-0.5 rounded-full text-xs font-medium"
                    :class="
                        selectedTags.length == 0 ||
                        selectedTags.indexOf(tag) !== -1
                            ? 'text-sky-900 bg-sky-200'
                            : 'text-gray-900 bg-gray-200'
                    "
                >
                    {{ tag }}
                </button>
            </ul>
        </div>
        <!-- TODO: List of `Article` -->
        <div class="flex flex-col gap-8 divide-y divide-gray-100">
            <ul
                v-for="article in sortDirection
                    ? matchTags(articles, selectedTags, search)
                    : articles.slice().reverse()"
                :key="article"
            >
                <Article :article="article" :selectedTags="selectedTags" />
            </ul>
        </div>
    </div>
</template>

<script setup>
import { ref } from "vue";

const sortDirection = ref(true);
const selectedTags = ref([]);
const search = ref("");

function filterTag(tag) {
    const index = selectedTags.value.indexOf(tag);

    if (index !== -1) {
        selectedTags.value.splice(index, 1);
    } else {
        selectedTags.value.push(tag);
    }
}

function matchTags(articles, selectedTags, search) {
    if (selectedTags.length === 0 && search.length === 0) {
        return articles;
    }
    const matches = [];

    if (selectedTags.length === 0) {
        matches.push(...articles);
    } else {
        articles.forEach((article) => {
            if (article.tags.some((v) => selectedTags.indexOf(v) !== -1)) {
                matches.push(article);
            }
        });
    }
    if (search.length === 0) {
        return matches;
    }
    return matches.filter((article) =>
        article.title.toLowerCase().includes(search.toLowerCase())
    );
}

const { data: articles } = await useAsyncData("articles", () => {
    // TODO: Fetch articles from `content/` ordered by date DESC
    // https://content.nuxtjs.org/api/composables/query-content#find
    return new Promise((resolve) => {
        queryContent("articles")
            .sort({ date: -1 }) // why is it -1 and not 0 like on the doc ? --> https://content.nuxtjs.org/api/composables/query-content#sortoptions
            .find()
            .then((articles) => resolve(articles));
    });
});

const { data: tags } = await useAsyncData("tags", async () => {
    // TODO: Fetch articles from `content/` ordered by date DESC
    // https://content.nuxtjs.org/api/composables/query-content#find
    const tags = [];

    await articles._rawValue.forEach(async (article) => {
        await article.tags.forEach(async (tag) => {
            if (!tags.includes(tag)) {
                tags.push(tag);
            }
        });
    });

    return tags;
});
</script>
