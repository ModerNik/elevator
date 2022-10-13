<!-- Кабина лифта для маштабируемой системы -->

<template>
    <div :id="'cabin-'+elevator" class="cabina"></div>
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
</style>