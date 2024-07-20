<script setup lang="ts">
</script>

<template>
    <div class="panel-row-container">
        <div class="leftpanel">left</div>
        <div class="grip"></div>
        <div class="rightpanel">right</div>
    </div>
</template>

<style lang="css" scoped>
.panel-row-container {
    width: 100%;
    height: 100%;
    margin: 0;
    padding: 0;
    box-sizing: border-box;

    display: grid;
    grid-template-columns: 1fr 0.5rem 1fr;
}

.leftpanel {
    background-color: rgb(213, 243, 238);
}

.grip {
    background-color: rgb(188, 188, 188);
}

.rightpanel {
    background-color: rgb(213, 235, 245);
}
</style>
