<template>
  <div class="grid grid-cols-1 md:grid-cols-2 gap-8 w-full max-w-6xl mx-auto px-4">
    <router-link
      v-for="link in articles"
      :key="link.name"
      :to="{ name: link.name }"
      class="group relative flex flex-col overflow-hidden rounded-2xl bg-white dark:bg-gray-800 shadow-lg hover:shadow-2xl transition-all duration-500 ease-out"
    >
      <div class="relative overflow-hidden aspect-[4/3]">
        <img
          :src="link?.meta?.image || 'https://images.unsplash.com/photo-1517694712202-14dd9538aa97?w=800&q=80'"
          :alt="link?.meta?.name ?? link?.meta?.title ?? link.name"
          class="w-full h-full object-cover transition-transform duration-700 ease-out group-hover:scale-110"
          loading="lazy"
        />
        <div class="absolute inset-0 bg-gradient-to-t from-black/70 via-black/20 to-transparent" />
        <div class="absolute bottom-0 left-0 right-0 p-6">
          <h2 class="text-2xl font-serif font-bold text-white leading-tight mb-2 drop-shadow-sm">
            {{ link?.meta?.name ?? link?.meta?.title ?? link.name }}
          </h2>
          <p v-if="config.description && link?.meta?.description" class="text-sm text-gray-200 line-clamp-2 leading-relaxed">
            {{ link?.meta?.description }}
          </p>
        </div>
      </div>
      <div class="flex items-center justify-between px-6 py-4">
        <div class="flex items-center gap-3">
          <span v-if="config.date && link?.meta?.date" class="text-xs font-medium text-gray-500 dark:text-gray-400 tracking-wide uppercase">
            {{ new Date(link?.meta?.date)?.toLocaleDateString('en-US', { year: 'numeric', month: 'short', day: 'numeric' }) }}
          </span>
          <span
            v-if="config.tags && link?.meta?.tags"
            v-for="tag in link?.meta?.tags"
            class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-primary-100 text-primary-700 dark:bg-primary-900/40 dark:text-primary-300"
          >
            {{ tag }}
          </span>
        </div>
        <div class="text-gray-400 dark:text-gray-500 group-hover:text-primary-500 dark:group-hover:text-primary-400 transition-colors duration-300">
          <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5 transition-transform duration-300 group-hover:translate-x-1" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M17 8l4 4m0 0l-4 4m4-4H3" />
          </svg>
        </div>
      </div>
    </router-link>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';
import sortBy from 'lodash/sortBy';

const config = {
  description: true,
  date: true,
  tags: false
};

const router = useRouter();
const routes = router.getRoutes();
const articles = sortBy(
  routes.filter(x => x.name && x.meta && x.path !== '/' && x.name !== 'all'),
  'meta.date'
).reverse();
</script>
