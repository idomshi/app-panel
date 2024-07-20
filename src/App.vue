<script setup lang="ts">
import { computed, ref } from 'vue';

const panelwidthpx = ref(200);
const panelwidth = computed(() => `${panelwidthpx.value}px`)

const pointerId = ref(-1)
const isDragging = ref(false)
const beginPosition = ref(0)
function dragstart(ev: PointerEvent) {
    if (isDragging.value) return;
    const target = ev.target
    if (!(target instanceof HTMLDivElement)) return
    target.setPointerCapture(pointerId.value = ev.pointerId)
    isDragging.value = true
    beginPosition.value = ev.pageX
}

function dragmove(ev: PointerEvent) {
    if (!isDragging.value) return;
    if (ev.pointerId !== pointerId.value) return;
    panelwidthpx.value += ev.pageX - beginPosition.value
    beginPosition.value = ev.pageX
}

function dragend(ev: PointerEvent) {
    if (!isDragging.value) return;
    if (ev.pointerId !== pointerId.value) return;
    const target = ev.target
    if (!(target instanceof HTMLDivElement)) return
    target.releasePointerCapture(pointerId.value)
    isDragging.value = false
    panelwidthpx.value += ev.pageX - beginPosition.value
}
</script>

<template>
    <div class="panel-row-container">
        <div class="leftpanel">left</div>
        <div class="grip"
            @pointerdown="dragstart"
            @pointermove="dragmove"
            @pointerup="dragend"
        ></div>
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
    grid-template-columns: v-bind("panelwidth") 1rem auto;
}

.leftpanel {
    background-color: rgb(213, 243, 238);
}

.grip {
    background-color: rgb(188, 188, 188);
    touch-action: none;
}

.rightpanel {
    background-color: rgb(213, 235, 245);
}
</style>
