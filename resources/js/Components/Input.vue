<script setup>
import { onMounted, ref } from 'vue';

defineProps(['modelValue']);

defineEmits(['update:modelValue']);

const input = ref(null);

onMounted(() => {
    if (input.value.hasAttribute('autofocus')) {
        input.value.focus();
    }
});
</script>

<template>
    <input class="border-gray-300 focus:border-gray-400 focus:ring focus:ring-teal-600 focus:ring-opacity-30 rounded-md shadow-sm my-3" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)" ref="input">
</template>
