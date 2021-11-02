<script setup>
import { ref } from '@vue/reactivity';

import SearchBox from './components/search-box.vue';
import SearchResults from './components/search-results.vue';

const userName = ref('');
const done = ref(true);

function search(name) {
	userName.value = name;
	done.value = false;
}
</script>

<template>
	<div class="pb-12 bg-gray-50">
		<div class="bg-gradient-to-tr from-gray-700 to-gray-900 py-16">
			<div class="w-11/12 md:w-8/12 mx-auto">
				<h1 class="text-white text-6xl font-semibold">Shiik</h1>
				<p class="text-gray-200 mt-1 uppercase">Check if a username is available in the top major social apps.</p>
				<search-box class="mt-8" @check="search" :done="done" />
			</div>
		</div>
		<SearchResults :userName="userName" @done="done = true" />
	</div>
</template>

<style></style>
