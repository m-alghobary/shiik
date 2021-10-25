<script setup>
import ServiceCard from './service-card.vue';

const props = defineProps({
	userName: String,
	services: Array,
});
</script>

<template>
	<h3 class="text-center mt-12 text-2xl">Search results</h3>
	<div class="bg-gray-50 p-6 mt-4 max-w-5xl mx-auto rounded-lg shadow-md grid grid-cols-5 gap-4">
		<ServiceCard v-for="service in props.services" :key="service.service" :userName="props.userName" :service="service" />
	</div>
</template>

<style lang="scss" scoped></style>
