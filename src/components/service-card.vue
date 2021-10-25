<script setup>
import { computed, onBeforeMount, ref, watch } from '@vue/runtime-core';

const props = defineProps({
	userName: String,
	service: Object,
});

const result = ref({});
const loading = ref(false);

loading.value = true;

watch(
	() => props.userName,
	(val) => {
		const endpoint = props.service.endpoint.replace('{username}', val);
		fetch(`https://api.instantusername.com${endpoint}`)
			.then((res) => res.json())
			.then((data) => (result.value = data))
			.finally(() => (loading.value = false));
	},
	{
		immediate: true,
	}
);

const border = computed(() => {
	let border = 'border-2 ';
	border += result.value?.available ? 'border-green-400' : 'border-red-400 opacity-50 shadow-none';
	return loading.value ? '' : border;
});
</script>

<template>
	<div class="bg-white shadow rounded p-6" :class="[border]">
		<span class="text-center text-blue-600 font-medium text-lg block">{{ props.service.service }}</span>
		<span v-if="loading" class="text-center block text-gray-400 text-sm mt-2">Loading..</span>
		<span v-else class="text-center block text-gray-600 mt-2">
			{{ result.available ? 'Available' : 'Taken' }}
		</span>
	</div>
</template>

<style lang="scss" scoped></style>
