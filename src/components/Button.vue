<template>
    <button 
    :type="type" 
    >
        <slot></slot>
        {{ name }}
    </button>
</template>

<script>
export default {
    props: ["type", "name"]
}
</script>