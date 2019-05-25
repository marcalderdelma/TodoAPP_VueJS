<template>
    <ul>
        <slot name="task"></slot>
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
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-auto-rows: auto;
        grid-gap: 1em;
    }
</style>
