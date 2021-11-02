<script setup>
import { ref } from 'vue';

const props = defineProps({
	done: Boolean
});

const userName = ref('');

const emit = defineEmits(['check']);

function check() {
	emit('check', userName.value);
}
</script>

<template>
	<div class="mt-1 relative rounded-md shadow-sm">
		<label for="user-name" class="block mb-2 text-gray-200">Check for username</label>
		<div class="mt-1 flex rounded-md shadow-sm relative">
			<div
				v-show="!props.done"
				class="
					w-full
					h-full
					absolute
					inset-0
					bg-gradient-to-r
					from-green-400
					to-blue-500
					rounded-md
					opacity-40
					grid
					place-items-center
				"
			>
				<span class="text-sm text-white italic">Loading...</span>
			</div>
			<input
				v-model="userName"
				type="text"
				id="user-name"
				class="py-3 flex-1 block w-full rounded-none rounded-l-md sm:text-sm border-gray-300 focus:outline-none"
				placeholder="Type your username..."
			/>
			<button
				class="
					inline-flex
					items-center
					px-6
					rounded-r-md
					border border-l-0 border-blue-500
					text-white
					bg-gradient-to-r
					from-green-400
					to-blue-500
					hover:from-blue-500 hover:to-green-500
					transition-colors
					duration-200
					uppercase
				"
				@click="check"
			>
				Check
			</button>
		</div>
	</div>
</template>

<style lang="scss" scoped></style>
