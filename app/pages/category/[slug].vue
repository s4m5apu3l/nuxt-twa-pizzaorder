<script setup lang="ts">
definePageMeta({
	validate: async (route) => {
		return typeof route.params.slug === 'string' && isNaN(parseInt(route.params.slug, 10));
	},
});

const route = useRoute();
// $fetch(`/api/products?category=${route.params.slug}`)
const { data: products, status } = useAsyncData(`${route.params.slug}`, async () => {
	return await $fetch(`/api/products`);
});
</script>

<template>
	<div class="py-4">
		<section class="max-w-[768px] mx-auto">
			<main-categories />
		</section>
		<section class="l-wrapper !mt-4">
			<product-list :status="status">
				<product-card v-for="product in products" :key="product.id" :data="product" />
			</product-list>
		</section>
	</div>
</template>
