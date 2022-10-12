<!-- Кабина лифта для маштабируемой системы -->

<template>
    <div id="cabin" class="cabina" :key="'cabin-'+elevator"></div>
</template>

<script>
export default {
    name: 'ElevatorShaft',
    props: {
        moving: {
            type: Boolean,
            default: false
        },
        floor: String,
        elevator: String
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