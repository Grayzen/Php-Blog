<template>
    <textarea class="border-gray-300 focus:border-gray-400 focus:ring focus:ring-teal-600 focus:ring-opacity-30 rounded-md shadow-sm my-3 px-3 py-2" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)" ref="textarea"></textarea>
</template>

<script>
export default {
    props: ['modelValue'],

    emits: ['update:modelValue'],

    methods: {
        focus() {
            this.$refs.textarea.focus()
        }
    }
}
</script>
