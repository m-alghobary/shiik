<script setup>
import { ref } from '@vue/reactivity';
import { watch } from '@vue/runtime-core';
import ServiceCard from './service-card.vue';

const services = [
	{
		service: 'Instagram',
		endpoint: '/check/instagram/{username}'
	},
	{
		service: 'TikTok',
		endpoint: '/check/tiktok/{username}'
	},
	{
		service: 'Twitter',
		endpoint: '/check/twitter/{username}'
	},
	{
		service: 'Facebook',
		endpoint: '/check/facebook/{username}'
	},
	{
		service: 'YouTube',
		endpoint: '/check/youtube/{username}'
	},
	{
		service: 'GitHub',
		endpoint: '/check/github/{username}'
	},
	{
		service: 'Quora',
		endpoint: '/check/quora/{username}'
	},
	{
		service: 'Behance',
		endpoint: '/check/behance/{username}'
	},
	{
		service: 'Pinterest',
		endpoint: '/check/pinterest/{username}'
	},
	{
		service: 'Spotify',
		endpoint: '/check/spotify/{username}'
	},
	{
		service: 'Telegram',
		endpoint: '/check/telegram/{username}'
	},
	{
		service: 'Vimeo',
		endpoint: '/check/vimeo/{username}'
	}
];

const doneCount = ref(0);

const emit = defineEmits(['done']);

watch(doneCount, (val) => {
	if (val === services.length) {
		emit('done', true);
	}
});

watch(
	() => props.userName,
	() => (doneCount.value = 0)
);

const props = defineProps({
	userName: String
});
</script>

<template>
	<div class="mt-8 w-11/12 md:w-8/12 mx-auto grid grid-cols-3 gap-4">
		<ServiceCard v-for="service in services" :key="service.service" :userName="props.userName" :service="service" @done="doneCount++" />
	</div>
</template>

<style lang="scss" scoped></style>
