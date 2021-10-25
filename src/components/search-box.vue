<script setup>
const props = defineProps({
	modelValue: String,
});

const emit = defineEmits(['update:modelValue']);

function updateValue(value) {
	emit('update:modelValue', value);
}
</script>

<template>
	<div class="bg-gray-50 py-10 max-w-5xl mx-auto mt-6 rounded-lg shadow-md">
		<div class="mt-1 w-10/12 mx-auto relative rounded-md shadow-sm">
			<label for="price" class="block mb-2 text-center text-xl font-medium text-gray-700">Check Username</label>
			<input
				:value="props.modelValue"
				type="text"
				name="price"
				id="price"
				class="focus:ring-blue-500 focus:border-blue-500 block w-full py-3 pl-7 pr-12 text-lg border-gray-300 rounded-md font-light"
				placeholder="Username..."
				@input="updateValue($event.target.value)"
			/>
		</div>
	</div>
</template>

<style lang="scss" scoped></style>
