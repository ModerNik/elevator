<template>
    <div class="building">
        <div class="column">
            <div class="cell">5</div>
            <div class="cell">4</div>
            <div class="cell">3</div>
            <div class="cell">2</div>
            <div class="cell">1</div>
        </div>
        <div class="column"><div class="cabine"></div></div>
        <div class="column">
            <div class="button_box"><FloorButton floor="5"></FloorButton></div>
            <div class="button_box"><FloorButton floor="4"></FloorButton></div>
            <div class="button_box"><FloorButton floor="3"></FloorButton></div>
            <div class="button_box"><FloorButton floor="2"></FloorButton></div>
            <div class="button_box"><FloorButton floor="1"></FloorButton></div>
        </div>
    </div>
</template>

<script>
//let buttons_queue = [];
//var current_floor = 1;

import FloorButton from './components/FloorButton.vue'
export default {
    name: "App",
    components: {
        FloorButton
    },
    methods: {
        
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
    vertical-align: top;
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
