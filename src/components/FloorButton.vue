<!-- Кнопки вызова лифта для маштабируемой системы -->

<template>
    <div class="button_box" :key="floor.id" v-for="floor in floors">
        <button :id="'button-'+floor" @click="button_push(floor)" class="floor_button">{{floor}}</button>
    </div>
</template>

<script>
//import { ref, onMounted } from "vue"; :ref="(el) => (buttons[i] = el)
export default {
    name: 'FloorButton',
    props: {
        floors: Array,
    },
    emits: ['floor-call'],
    /*data() {
        var buttons = ref([]);
        onMounted(() =>{
            console.log(buttons.value);
        });
        return {
            buttons,
        }
    },*/
    methods: {
        button_push(floor) {
            this.$emit('floor-call', floor);
        }
    },
}
</script>