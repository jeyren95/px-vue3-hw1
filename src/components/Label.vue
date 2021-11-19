<template>
    <label :for="id" class="block text-sm font-medium text-gray-700 sm:mt-px sm:pt-2">{{ label }}</label>
</template>

<script>
export default {
    props: ["id", "label"]
}
</script>