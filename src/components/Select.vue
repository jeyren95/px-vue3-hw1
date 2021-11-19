<template>
    <select 
    class="block w-full pl-3 pr-10 py-2 text-base border-gray-300 focus:outline-none focus:ring-pink-500 focus:border-pink-500 sm:text-sm rounded-md"
    :id="id" 
    :required="required" 
    :name="name"
    @change="handleChange"
    :value="modelValue"
    >
        <option v-for="(option, index) in selectOptions" :key="index" :value="option">
            {{ option }}
        </option>
    </select>   
</template>

<script>
export default {
    props: ["id", "required", "name", "selectOptions", "modelValue"],
    methods: {
        handleChange(e) {
            this.$emit("update:model-value", e.target.value)
        }
    }
}
</script>