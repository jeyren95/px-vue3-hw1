<template>
    <input 
    class="block w-full shadow-sm sm:text-sm focus:ring-pink-500 focus:border-pink-500 border-gray-300 rounded-md"
    :id="id"
    :name="name"
    :required="required"
    :type="type"
    :value="modelValue"
    @input="handleInput"
    />
</template>

<script>
export default {
    props: ["id", "name", "required", "type", "modelValue"],
    methods: {
        handleInput(e) {
            this.$emit("update:modelValue", e.target.value)
        }
    }
}
</script>