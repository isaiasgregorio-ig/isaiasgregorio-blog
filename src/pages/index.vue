<template>
	<div class="prose dark:prose-dark mb-16">
		<Title>
			Blog
			<template v-slot:description>Blog personal de Isaias Gregorio.</template>
		</Title>
	</div>
	<PostList />
	<div class="h-32"></div>
</template>

<script setup>
import { useHead } from '@vueuse/head';

useHead({
	title: 'Blog | Isaias Gregorio',
	meta: [{ name: 'description', content: 'Blog personal de Isaias Gregorio' }]
});
</script>

<route>
{
	meta: {
		layout: "home"
	}
}
</route>
