<!-- Кабина лифта для маштабируемой системы -->

<template>
    <div :id="'cabin-'+elevator" class="cabina">
        <div :id="'indicator-'+elevator" class="indicator">1</div>
    </div>
</template>

<script>
export default {
    name: 'ElevatorCabin',
    props: {
        moving: Boolean,
        floor: {
            type: Number,
            default: 1
        },
        elevator: Number
    },
}
</script>

<style scoped>
.cabina {
    position: absolute;
    margin-left: 3px;
    bottom: 0px;
    background-color: antiquewhite;
    height: 118px;
    width: 118px;
    transition: 1s;
}

.indicator {
    font-size: 20px;
    font-family: 'Courier New', Courier, monospace;
    margin: 0 auto;
    margin-top: 8px;
    background-color: dimgray;
    height: 20px;
    width: 60px;
    border-radius: 5px;
    color: aliceblue;
}
</style>