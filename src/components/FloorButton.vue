<!-- Прототип кнопок вызова лифта для маштабируемой системы -->

<template>
    <h2>{{floor}}</h2>
    <button id={{floor}} class="floor_button_style"/>
</template>

<script>
export default {
    name: 'FloorButton',
    props: {
        floor: String,
    }
}
</script>

<style scoped>
.floor_button_style {
    border-radius: 10%;
    background-color: bisque;
    width: 40px;
    height: 40px;
}
</style>