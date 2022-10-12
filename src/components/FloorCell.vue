<!-- Ячейка шахты лифта для маштабируемой системы -->

<template>
    <div class="cell" :key="floor.id" v-for="floor in floors">
        <hr class="divider">
    </div>
</template>

<script>
export default {
    name: 'FloorCell',
    props: {
        floors: Array
    },
}
</script>