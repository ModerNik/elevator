<template>
    <div class="building">
        <div class="column">
            <div><button @click="deleteFloor" class="delete_floor_button">-</button></div>
            <div><button @click="addFloor" class="add_floor_button">+</button></div>
        </div>
        <div class="column">
            <button @click="deleteElevator" class="delete_floor_button">-</button>
            <button @click="addElevator" class="add_floor_button">+</button>
        </div>
    </div>

    <div class="building">
        <ElevatorShaft :floors="floors" :elevators="elevators"/>
        <div class="column">
            <FloorButton @floor-call="floorCall" :floors="floors" />
        </div>
    </div>
</template>

<script>
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
            elevators: [],
            current_floors: [],
            buttons_queue: [],
        }
    },
    created() {
        this.floors = [5, 4, 3, 2, 1]
        this.elevators = [1, 2]
        this.current_floors = [1, 1]
        this.buttons_queue = []
    },
    methods: {
        floorCall(floor) {
            this.buttons_queue.push(floor);
            let temp_state = false;
            for (let i = 0; i < this.current_floors.length; i++) {
                if (this.current_floors[i] == floor) {
                    alert('On this floor');
                    this.buttons_queue.pop(1);
                    temp_state = true;
                    break;
                }
            }
            if (!temp_state) {
                console.log(this.buttons_queue);
                if (this.buttons_queue.length == 1) {
                    let min = this.floors.length;
                    let elevator_number = 0;
                    for (let i = 0; i < this.current_floors.length; i++) {
                        if (this.current_floors[i] > 0) {
                            if (Math.abs(this.current_floors[i] - floor) < min) {
                                min = Math.abs(this.current_floors[i] - floor)
                                elevator_number = i;
                            }
                        }
                    }
                    this.moveCabin(elevator_number, floor)
                    //this.buttons_queue.pop(0);
                    setTimeout((elevator_number) => this.current_floors[elevator_number] = this.buttons_queue[0], 1000 * (min + 3))
                }
            }
        },
        moveCabin(elevator_number, floor_to_move) {
            console.log('Elevator:', elevator_number, ' Moving to:', floor_to_move);
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
    margin-bottom: 40px;
    vertical-align: top;
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
