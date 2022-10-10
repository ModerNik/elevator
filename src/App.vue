<template>
    <div class="building">
        <div class="column">
            <div class="cell">5</div>
            <div class="cell">4</div>
            <div class="cell">3</div>
            <div class="cell">2</div>
            <div class="cell">1</div>
        </div>
        <div class="column">
            <div class="button_box"><button class="floor_button_style" id="button_5" floor="5"></button></div>
            <div class="button_box"><button class="floor_button_style" id="button_4" floor="4"></button></div>
            <div class="button_box"><button class="floor_button_style" id="button_3" floor="3"></button></div>
            <div class="button_box"><button class="floor_button_style" id="button_2" floor="2"></button></div>
            <div class="button_box"><button class="floor_button_style" id="button_1" floor="1"></button></div>
        </div>
    </div>
</template>
<!-- import FloorButton from './components/FloorButton' -->
<script>



export default {
    name: "App",
    components: {
},
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
</style>
