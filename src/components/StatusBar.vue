<template>
    <div class="status-bar">
        <slot></slot>
    </div>
</template>

<script>
    
</script>

<style scoped>
    .status-bar {
        border: 1px solid #9c9ca3;
        border-radius: 3px;
        height: 25px;
        width: 100%;
    }
    .status {
        height: 100%;
        background-color: hsla(125, 68%, 41%, 0.781);
    }
</style>
