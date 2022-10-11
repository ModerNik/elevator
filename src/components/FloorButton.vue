<!-- Кнопки вызова лифта для маштабируемой системы -->

<template>
    <div class="button_box" :key="floor.id" v-for="floor in floors">
        <button @click="button_push(floor)" class="floor_button_style" />
    </div>
</template>

<script>
export default {
    name: 'FloorButton',
    props: {
        floors: Array
    },
    emits: ['floor-call'],
    methods: {
        button_push(floor) {
            let buttons_queue = []
            buttons_queue.push(floor);
            this.$emit('floor-call', floor);
            setTimeout(() => {
                console.log(buttons_queue.pop(floor));
            },
                1000
            );
        }
    },
}
</script>