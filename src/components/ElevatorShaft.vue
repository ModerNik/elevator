<!-- Шахта лифта для маштабируемой системы -->

<template>
    <div class="column" :key="elevator.id" v-for="elevator in elevators">
        <FloorCell :floors="floors"/>
        <ElevatorCabin :elevator="elevator"/>
    </div>
</template>

<script>
import ElevatorCabin from './ElevatorCabin.vue'
import FloorCell from './FloorCell.vue'
export default {
    name: 'ElevatorShaft',
    props: {
        elevators: Array,
        floors: Array
    },
    components: {
        FloorCell,
        ElevatorCabin
    },
}
</script>