<script setup>
import { computed, ref, watch } from '@vue/runtime-core';

const props = defineProps({
	userName: String,
	service: Object
});

const emit = defineEmits(['done']);

const result = ref({});
const loading = ref(false);
const dirty = ref(false);

watch(
	() => props.userName,
	(val) => {
		if (!val) return;

		loading.value = true;
		dirty.value = true;
		const endpoint = props.service.endpoint.replace('{username}', val);
		fetch(`https://api.instantusername.com${endpoint}`)
			.then((res) => res.json())
			.then((data) => (result.value = data))
			.finally(() => {
				loading.value = false;
				emit('done', true);
			});
	},
	{
		immediate: true
	}
);

const available = computed(() => {
	return dirty.value ? !!result.value?.available : true;
});
</script>

<template>
	<div class="bg-white shadow-md rounded p-8" :class="{ 'opacity-50': !available }">
		<span class="text-center text-gray-800 font-medium text-xl block">{{ props.service.service }}</span>
		<span v-if="loading" class="text-center block text-gray-400 text-sm mt-2">Loading..</span>
		<span v-else-if="!dirty" class="text-center block text-gray-400 text-sm mt-2">???</span>
		<span v-else class="text-center block text-gray-600 mt-2">
			<span v-if="result.available" class="text-green-500">Available</span>
			<span v-else class="text-red-500">Taken</span>
		</span>
	</div>
</template>

<style lang="scss" scoped></style>
