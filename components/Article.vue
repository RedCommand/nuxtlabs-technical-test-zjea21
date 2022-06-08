<template>
  <div class="pt-8">
    <div class="flex items-center gap-3">
      <!-- TODO: Display article tags -->
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
        </p>
      </div>
    </div>
  </div>
</template>

<script setup>
// TODO: Get `article` from props
// https://vuejs.org/api/sfc-script-setup.html#defineprops-defineemits
const article = ref({
  _path: '',
  title: '',
  description: '',
  author: {},
});
</script>
