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
        <ElevatorShaft :floors="floors" :elevators="elevators" />
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
            moving: Boolean,
            floors: [],
            elevators: [],
            current_floors: [],
            buttons_queue: [],
        }
    },
    created() {
        this.floors = [5, 4, 3, 2, 1]
        this.elevators = [1]
        this.current_floors = [1]
        this.buttons_queue = []
        this.moving = false;
    },
    methods: {
        floorCall(floor) {
            if (floor) {
                this.buttons_queue.push(floor);
            } else {
                console.log('Приехал');
                this.moving = false;
            }
            if (this.buttons_queue.length != 0 && !this.moving) {
                let temp_state = true;
                for (let i = 0; i < this.current_floors.length; i++) {
                    if (this.current_floors[i] == this.buttons_queue[0]) {
                        this.buttons_queue.shift();
                        temp_state = false;
                        this.floorCall(0);
                        break;
                    }
                }
                if (temp_state) {
                    this.moveCabin();
                    for (let i = 0; i < this.current_floors.length; i++) {
                        this.current_floors[i] = this.buttons_queue[0];
                    }
                    console.log('Очередь:', this.buttons_queue);
                    this.buttons_queue.shift();
                }
            }
        },
        moveCabin() {
            this.moving = true;
            console.log('Moving to:', this.buttons_queue[0]);
            var lifting_time = Math.abs(this.buttons_queue[0] - this.current_floors[0]);
            document.getElementById("cabin").style.transition = (lifting_time) + 's';
            document.getElementById("cabin").style.bottom = this.buttons_queue[0] * 120 - 120 + 'px';
            setTimeout(() => this.relax(), lifting_time*1000);
            setTimeout(() => this.floorCall(0), lifting_time*1000+3000);
        },

        relax(){
            document.getElementById("cabin").style.transition = '1.5s';
            document.getElementById("cabin").style.opacity = '0.2';
            setTimeout(() =>document.getElementById("cabin").style.opacity = '1', 1500);
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
            this.buttons_queue.splice(0,this.buttons_queue.length);
            this.floorCall(1);
        },
        addElevator() {
            if (this.elevators.length >= 10) {
                alert('Куда столько? 0_о');
            } else {
                this.elevators.push(this.elevators.length + 1);
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
    color: #303030;
    margin-top: 20px;
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

.cabin {
    position: absolute;
    margin-left: 3px;
    bottom: 0px;
    background-color: antiquewhite;
    height: 120px;
    width: 118px;
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
    transition: 250ms;
}

.floor_button_style:hover {
    background-color: beige;
    transition: 250ms;
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
    transition: 250ms;
}

.add_floor_button:hover {
    background-color: limegreen;
    transition: 250ms;
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
    transition: 250ms;
}

.delete_floor_button:hover {
    background-color: brown;
    transition: 250ms;
}
</style>
