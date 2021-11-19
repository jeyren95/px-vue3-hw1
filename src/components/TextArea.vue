<template>
    <textarea 
    class="
    block 
    w-full 
    shadow-sm 
    sm:text-sm 
    focus:ring-pink-500 
    focus:border-pink-500 border 
    border-gray-300 
    rounded-md
    "
    :id="id" 
    :name="name" 
    :rows="rows" 
    :required="required"
    @input="handleInput"
    :value="modelValue"
    >
    </textarea>
</template>

<script>
export default {
    props: ["id", "name", "rows", "required", "modelValue"],
    methods: {
        handleInput(e) {
            this.$emit("update:modelValue", e.target.value)
        }
    }
}
</script>