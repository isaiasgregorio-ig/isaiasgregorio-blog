<template>
	<div class="prose dark:prose-dark mb-16">
		<Title>
			A Blog Template
			<template v-slot:description>This is a blog template with a description.</template>
		</Title>
	</div>
	<PostList />
	<div class="h-32"></div>
</template>

<script setup>
import { useHead } from '@vueuse/head';

useHead({
	title: 'Blog',
	meta: [{ name: 'description', content: 'Blog example description' }]
});
</script>

<route>
{
	meta: {
		layout: "home"
	}
}
</route>
