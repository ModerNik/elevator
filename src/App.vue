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
                    this.changeButtonColor('wait', call_floor);
                } else {
                    return;
                }
            } else {
                console.log('??????????????');
                console.log('??????????????:', this.buttons_queue);
            }
            if (this.buttons_queue.length != 0) {
                if (call_floor == 0) {
                    let sum = 0;
                    for (let i = 0; i < this.current_floors.length; i++) {
                        if (this.current_floors[i] == 0) {
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
                if (cabin_number) {
                    this.moveCabin(cabin_number, call_floor);
                    console.log('??????????????:', this.buttons_queue);
                }
            }
        },
        moveCabin(cabin_number, floor_to_move) {
            var cabinID = 'cabin-' + cabin_number;
            var cabin = document.getElementById(cabinID);
            this.changeButtonColor('coming', floor_to_move);
            console.log('Moving to:', floor_to_move);
            var lifting_time = Math.abs(floor_to_move - this.current_floors[cabin_number - 1]);
            cabin.style.transition = (lifting_time) + 's';
            var indicator = 'indicator-'+cabin_number;
            var indicator_change
            if (this.current_floors[cabin_number-1]-floor_to_move > 0){
                indicator_change = '???';
            } else {
                indicator_change = '???';
            }
            indicator_change += ' '+floor_to_move;
            document.getElementById(indicator).innerHTML = indicator_change;
            cabin.style.bottom = floor_to_move * 120 - 120 + 'px';
            setTimeout(() => this.relax(cabin_number), lifting_time * 1000);
            setTimeout(() => this.buttons_queue.splice(this.buttons_queue.indexOf(floor_to_move), 1), lifting_time * 1000 + 3000);
            this.current_floors[cabin_number - 1] = 0;
            setTimeout(() => this.current_floors[cabin_number - 1] = floor_to_move, lifting_time * 1000 + 3000);
            setTimeout(() => this.floorCall(0), lifting_time * 1000 + 3000);
            setTimeout(() => this.changeButtonColor('free', floor_to_move), lifting_time * 1000 + 3000);
        },

        relax(cabin_number) {
            var cabinID = 'cabin-' + cabin_number;
            var cabin = document.getElementById(cabinID);
            cabin.style.transition = '1.5s';
            cabin.style.opacity = '0.2';
            setTimeout(() => cabin.style.opacity = '1', 1500);
        },

        changeButtonColor(command, button_number) {
            let buttonID = 'button-' + button_number;
            let target;
            try {
                target = document.getElementById(buttonID).className;
                console.log(target);
            }
            catch (err) {
                for (let i = 0; i < this.floors.length; i++) {
                    buttonID = 'button-' + (i + 1);
                    document.getElementById(buttonID).className = "floor_button";
                }
            }
            switch (command) {
                case 'wait':
                    document.getElementById(buttonID).className = "floor_button_wait";
                    break;
                case 'coming':
                    document.getElementById(buttonID).className = "floor_button_coming";
                    break;
                case 'free':
                    document.getElementById(buttonID).className = "floor_button";
                    break;
                default:
                    document.getElementById(buttonID).className = "floor_button";
                    break;
            }
        },

        addFloor() {
            if (this.floors.length == 7) {
                alert('?? ???????????? ?????????????? ?????????????????????? 7-?? ??????????????, ?? ?????? ?????????????? ?????????????????????? ????????????????. ;D');
            } else {
                this.floors.unshift(this.floors.length + 1);
            }
        },
        deleteFloor() {
            if (this.floors.length > 2) {
                this.floors.shift();
                for (let i = 0; i < this.floors.length; i++) {
                    let buttonID = 'button-' + (i + 1);
                    document.getElementById(buttonID).className = "floor_button";
                }
                this.buttons_queue.splice(0, this.buttons_queue.length);
                for (let i = 0; i < this.current_floors.length; i++) {
                    this.current_floors[i] = 1;
                    var cabinID = 'cabin-' + (i + 1);
                    var cabin = document.getElementById(cabinID);
                    cabin.style.bottom = '0px';
                    let indicator = 'indicator-'+(i+1);
                    document.getElementById(indicator).innerHTML = '1';
                }
            } else {
                alert('?????????? ???????????? ???????? ?? ?????????????????????? ?????????????');
            }
        },
        addElevator() {
            if (this.elevators.length >= 10) {
                alert('???????? ??????????????? 0_??');
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
                alert('???? ???????? 1 ???? ?????????? ????????????????.');
            }
        },
    }
};
</script>

<style>
    @import './styles/App.css';
</style>