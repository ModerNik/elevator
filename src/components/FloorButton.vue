<!-- Прототип кнопок вызова лифта для маштабируемой системы -->

<template>
    <button @click="button_push(floor)" class="floor_button_style" />
</template>

<script>
export default {
    name: 'FloorButton',
    props: {
        floor: String
    },
    methods: {
        button_push(floor) {
            let buttons_queue = []
            buttons_queue.push(floor);
            setTimeout(() => {
                console.log(buttons_queue.shift(floor));
            },
                1000
            );
        }
    },
}
</script>