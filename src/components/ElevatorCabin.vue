<!-- Шахта лифта для маштабируемой системы -->

<template>
    <div class="cabin" :key="floor" ref="elevator">
    </div>
</template>

<script>
export default {
    name: 'ElevatorShaft',
    props: {
        moving: {
            type: Boolean,
            default: false
        },
        floor: String
    },
}
</script>

<style>
.cabin {
    position: absolute;
    margin-left: 3px;
    bottom: 0px;
    background-color: antiquewhite;
    height: 120px;
    width: 118px;
}
</style>