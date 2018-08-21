<template>
    <div class="start-border">
        <div class="horiz-crop"></div>
        <div class="vert-crop"></div>
        <div class="btn-start">
            СТАРТ
        </div>
        <a target="_blank" href="https://metanit.com/" class="start-stream">
            Начать показ
        </a>
    </div>
</template>

<script>
    export default {
        name: "start"
    }
</script>

<style scoped>
    .start-border {
        position: relative;
        height: 600px;
        width: 840px;
        border: 5px solid #FFD100;

    }

    .horiz-crop, .vert-crop {
        position: absolute;
        background-color: #031323;
    }

    .horiz-crop {
        top: 100px;
        left: -5px;
        height: 400px;
        width: 850px;
    }

    .vert-crop {
        top: -5px;
        left: 100px;
        height: 610px;
        width: 640px;
    }

    .btn-start {
        position: absolute;
        top: 100px;
        left: 125px;
        height: 370px;
        width: 370px;
        background-color: #FFD100;
        border: 15px solid white;
        border-radius: 200px;
        text-align: center;
        line-height: 370px;
        font-family: 'Bender-Black', sans-serif;
        color: black;
        font-size: 80px;
        cursor: pointer;
    }

    a, a:visited, a:active {
        color: white;
        text-decoration: none;
    }

    a:hover {
        text-decoration: underline;
    }

    .start-stream {
        position: absolute;
        top: 220px;
        right: 65px;
        width: 200px;
        font-family: 'Bender', sans-serif;
        font-size: 60px;
    }
</style>