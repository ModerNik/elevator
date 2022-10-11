<!-- Шахта лифта для маштабируемой системы -->

<template>
    <div class="column" :key="elevator.id" v-for="elevator in elevators">
        <FloorCell :floors="floors"/>
        <div class="cabine"/>
    </div>
</template>

<script>
import FloorCell from './FloorCell.vue'
export default {
    name: 'ElevatorShaft',
    props: {
        elevators: Array,
        floors: Array
    },
    components: {
        FloorCell
    }
}
</script>