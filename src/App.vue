<template>
    <div class="building">
        <ElevatorShaft :floors="floors" :elevators="elevators" />
        <div class="column">
            <FloorButton @floor-call="floorCall" :floors="floors" />
        </div>
        <div class="column">
            <div><button @click="addFloor" class="add_floor_button">+</button></div>
            <div><button @click="deleteFloor" class="delete_floor_button">-</button></div>
        </div>
        <div class="column">
            <button @click="deleteElevator" class="delete_floor_button">-</button>
            <button @click="addElevator" class="add_floor_button">+</button>
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
    },
    methods: {
        floorCall(floor) {
            console.log('Called ', floor)
        },
        addFloor() {
            if (this.floors.length == 7) {
                alert('В данном примере ограничимся 7-ю этажами, у нас элитный малоэтажный пентхаус. ;D');
            } else {
                this.floors.unshift(this.floors.length + 1);
            }
        },
        deleteFloor() {
            if (this.floors.length > 2) {
                this.floors.shift();
            } else {
                alert('Зачем делать лифт в одноэтажном здании?');
            }
        },
        addElevator() {
            if (this.elevators.length == 10) {
                alert('Куда столько? 0_о');
            } else {
                this.elevators.push(this.floors.length + 1);
            }
        },
        deleteElevator() {
            if (this.elevators.length > 1) {
                this.elevators.pop();
            } else {
                alert('Ну хоть 1 то нужно оставить.');
            }
        },
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
    position: relative;
    text-align: center;
    height: 120px;
    margin-right: 10px;
    margin-left: 10px;
}

.cell {
    height: 120px;
    width: 120px;
    border-left-style: solid;
    border-right-style: solid;
    border-width: 2px;
    border-color: #808080;
}

.floor_button_style {
    border-radius: 10%;
    background-color: bisque;
    width: 40px;
    height: 40px;
    border: none;
}

.floor_button_style:hover {
    background-color: beige;
}

.button_box {
    margin-bottom: 2px;
    height: 120px;
    width: 120px;
}

.cabine {
    position: absolute;
    margin-left: 3px;
    bottom: 0px;
    background-color: antiquewhite;
    height: 120px;
    width: 118px;
}

.add_floor_button {
    margin-top: 8px;
    margin-bottom: 8px;
    margin-left: 8px;
    margin-right: 8px;
    font-family: 'Courier New', Courier, monospace;
    font-size: 30px;
    color: white;
    border-radius: 10%;
    background-color: lawngreen;
    width: 40px;
    height: 40px;
    border: none;
}

.add_floor_button:hover {
    background-color: limegreen;
}

.delete_floor_button {
    margin-top: 8px;
    margin-bottom: 8px;
    margin-left: 8px;
    margin-right: 8px;
    font-family: 'Courier New', Courier, monospace;
    font-size: 30px;
    color: white;
    border-radius: 10%;
    background-color: crimson;
    width: 40px;
    height: 40px;
    border: none;
}

.delete_floor_button:hover {
    background-color: brown;
}
</style>
