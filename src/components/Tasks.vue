<template>
    <ul>
        <slot></slot>
    </ul>
</template>

<script>
export default {

}
</script>

<style scoped>
    ul {
        color: inherit;
        /* width: 80vw; */
        padding: 0;
        margin: 1em 0 0;
        list-style: none;
        display: flex;
        flex-wrap: wrap;
    }
</style>
