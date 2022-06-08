<template>
  <div>
    <div class="border-b sticky top-0 bg-white">
      <div class="max-w-3xl px-4 py-4 mx-auto sm:px-6 lg:px-8">
        <NuxtLink to="/" active-class="font-bold">Nuxt Blog</NuxtLink>
      </div>
    </div>

    <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8 pt-8 pb-16">
      <!-- TODO: Display the current nuxt page -->
      <NuxtPage/>
      <!--end todo-->
    </div>
  </div>
</template>
