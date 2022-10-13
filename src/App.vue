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
    },
    methods: {
        floorCall(floor) {
            let call_floor = floor;
            if (call_floor) {
                let temp_state = true;
                for (let i = 0; i < this.buttons_queue.length; i++) {
                    if (call_floor == this.buttons_queue[i]) {
                        temp_state = false;
                        break;
                    }
                }
                if (temp_state) {
                    for (let i = 0; i < this.current_floors.length; i++) {
                        if (call_floor == this.current_floors[i]) {
                            temp_state = false;
                            break;
                        }
                    }
                }
                if (temp_state) {
                    this.buttons_queue.push(call_floor);
                    console.log(this.buttons_queue);
                    //this.changeButtonColor(1, floor);
                } else {
                    return;
                }
            } else {
                console.log('Приехал');
                console.log(this.buttons_queue);
            }
            if (this.buttons_queue.length != 0) {
                if (call_floor == 0){
                    let sum = 0;
                    for (let i = 0; i < this.current_floors.length; i++){
                        if (this.current_floors[i] == 0){
                            sum++;
                        }
                    }
                    call_floor = this.buttons_queue[sum];
                }
                let cabin_number = 0;
                let min = this.floors.length;
                for (let i = 0; i < this.current_floors.length; i++) {
                    if (this.current_floors[i]) {
                        let distanse = Math.abs(this.current_floors[i] - call_floor);
                        if (distanse < min) {
                            min = distanse;
                            cabin_number = i + 1;
                        }
                    }
                }
                /*
                ToDo:
                    moving
                    button colors
                    Табло индикации движения
                    Save state???
                */
                //if (!cabin_number){ return; }
                if (cabin_number) {
                    this.moveCabin(cabin_number, call_floor);
                    console.log('Очередь:', this.buttons_queue);
                }
            }
        },
        moveCabin(cabin_number, floor_to_move) {
            console.log(cabin_number, floor_to_move);
            var cabinID = 'cabin-' + cabin_number;
            var cabin = document.getElementById(cabinID);
            //this.changeButtonColor(2, this.buttons_queue[0]);
            console.log('Moving to:', floor_to_move);
            var lifting_time = Math.abs(floor_to_move - this.current_floors[cabin_number - 1]);
            cabin.style.transition = (lifting_time) + 's';
            cabin.style.bottom = floor_to_move * 120 - 120 + 'px';
            setTimeout(() => this.relax(cabin_number), lifting_time * 1000);
            setTimeout(() => this.buttons_queue.splice(this.buttons_queue.indexOf(floor_to_move), 1), lifting_time * 1000 + 3000);
            this.current_floors[cabin_number - 1] = 0;
            setTimeout(() => this.current_floors[cabin_number - 1] = floor_to_move, lifting_time * 1000 + 3000);
            setTimeout(() => this.floorCall(0), lifting_time * 1000 + 3000);
            //this.changeButtonColor(3, this.buttons_queue[0]);
        },

        relax(cabin_number) {
            var cabinID = 'cabin-' + cabin_number;
            var cabin = document.getElementById(cabinID);
            cabin.style.transition = '1.5s';
            cabin.style.opacity = '0.2';
            setTimeout(() => cabin.style.opacity = '1', 1500);
        },

        /*changeButtonColor(command, buttonID) {
            switch (command) {
                case 1:
                    console.log('change', buttonID, 1);
                    console.log(this.buttonRefs[0]);
                    break;
                case 2:
                    console.log('change', buttonID, 2);
                    break;
                case 3:
                    console.log('change', buttonID, 3);
                    break;
            }
        },*/

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
            this.buttons_queue.splice(0, this.buttons_queue.length);
            this.floorCall(1);
        },
        addElevator() {
            if (this.elevators.length >= 10) {
                alert('Куда столько? 0_о');
            } else {
                this.elevators.push(this.elevators.length + 1);
                this.current_floors.push(1);
            }
        },
        deleteElevator() {
            if (this.elevators.length > 1) {
                this.elevators.pop();
                this.current_floors.pop();
            } else {
                alert('Ну хоть 1 то нужно оставить.');
            }
        },
    }
};
</script>

<style>
@import './styles/App.css';
</style>