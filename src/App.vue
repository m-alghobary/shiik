<script setup>
import { ref } from '@vue/reactivity';
import { watch } from '@vue/runtime-core';

import SearchBox from './components/search-box.vue';
import SearchResults from './components/search-results.vue';

const userName = ref('');
const services = ref([]);

watch(userName, () => {
	if (services.value.length) return;

	if (userName.value.trim()) {
		fetch('https://api.instantusername.com/services')
			.then((res) => res.json())
			.then((data) => (services.value = data));
	}
});
</script>

<template>
	<search-box v-model="userName" />
	<SearchResults :userName="userName" :services="services" />
</template>

<style></style>
