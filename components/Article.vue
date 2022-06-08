
<template>
    <div class="pt-8">
        <div class="flex items-center gap-3">
            <!-- TODO: Display article tags -->
            <span
                v-for="tag in article.tags"
                class="px-2 py-0.5 rounded-full text-xs text-sky-900 font-medium bg-sky-200"
                >{{ tag }}</span
            >
        </div>
        <a :href="article._path" class="block mt-4">
            <p class="text-xl font-semibold text-gray-900">
                {{ article.title }}
            </p>
            <p class="mt-1 text-base text-gray-500">
				{{ article.description }}
            </p>
        </a>
        <div v-if="article.author" class="mt-6 flex items-center">
            <div class="flex-shrink-0">
				<a :href="article.author.link" target="_blank">
                    <span class="sr-only">{{ article.author.name }}</span>
                    <img
                        class="h-10 w-10 rounded-full"
                        :src="article.author.avatarUrl"
                        alt=""
                    />
                </a>
            </div>
            <div class="ml-3">
				<p class="text-sm font-medium text-gray-900">
					<a :href="article.author.link" target="_blank">
                        {{ article.author.name }}
                    </a>
                </p>
                <p class="flex space-x-1 text-sm text-gray-500">
					<!-- TODO: Display formatted date -->
                    <a>{{ formatDate(article.date) }}</a>
                </p>
            </div>
        </div>
    </div>
</template>

<script setup>
// TODO: Get `article` from props
// https://vuejs.org/api/sfc-script-setup.html#defineprops-defineemits
import { formatDate } from '../utils/index.ts'

const props = defineProps({
	article: Object,
});

const article = ref({
	_path: props.article._path,
    title: props.article.title,
    description: props.article.description,
    author: props.article.author,
    date: props.article.date,
    tags: props.article.tags,
});
</script>
