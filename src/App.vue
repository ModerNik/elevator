<template>
    <div class="building">
        <ElevatorShaft :floors="floors" :elevators="elevators"/>
        <div class="column">
            <FloorButton :floors="floors"/>
        </div>
    </div>
</template>

<script>
//let buttons_queue = [];
//var current_floor = 1;
import ElevatorShaft from './components/ElevatorShaft.vue'
import FloorButton from './components/FloorButton.vue'

export default {
    name: "App",
    components: {
        FloorButton,
        ElevatorShaft
    },
    data() {
        return {
            floors: [],
            elevators: []
        }
    },
    created() {
        this.floors = [5, 4, 3, 2, 1]
        this.elevators = [1]
    }
};
</script>

<style>
#app {
    font-family: Verdana, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #303030;
    margin-top: 60px;
}

.building>div {
    vertical-align: bottom;
    display: inline-block;
    width: auto;
    height: auto;
}

.column {
    
    text-align: center;
    height: 120px;
    margin-right: 10px;
    margin-left: 10px;
}

.cell {
    margin-bottom: 2px;
    height: 120px;
    width: 120px;
    border-left-style: solid;
    border-right-style: solid;
    border-width: 2px;
    border-color: #808080;
}

.divider {
    margin-top: 0em;
    margin-bottom: 0em;
}

.floor_button_style {
    border-radius: 10%;
    background-color: bisque;
    width: 40px;
    height: 40px;
    border: none;
}
.floor_button_style:hover {
    border-radius: 10%;
    background-color:beige;
    width: 40px;
    height: 40px;
    border: none;
}

.button_box {
    margin-bottom: 2px;
    height: 120px;
    width: 120px;
}
.cabine {
    position: absolute;
    left: 20px;
    margin-top: 60px;
    top: 0px;
    background-color: antiquewhite;
    height: 120px;
    width: 118px;
}
</style>
