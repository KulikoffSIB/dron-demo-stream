<template>
    <div v-bind:class="[run ? 'start-border-lg': 'start-border']">
        <div v-bind:class="[run ? 'horiz-crop-lg': 'horiz-crop']"></div>
        <div v-bind:class="[run ? 'vert-crop-lg': 'vert-crop']"></div>
        <div class="video-stream" v-if="run">
            <iframe src="http://127.0.0.1:8086/cam.mjpg" frameborder="0"></iframe>
        </div>
        <template v-if="!run">
            <div class="btn-start" @click="start()">
                СТАРТ
            </div>
            <a target="_blank" href="#" class="start-stream" @click="start($event)">
                Начать показ
            </a>
        </template>
    </div>
</template>

<script>
    import {config} from "../dron-config";

    export default {
        name: "start",
        data: function () {
            return {
                run: false
            }
        },
        methods: {
            start(event) {
                if (event) event.preventDefault();

                window.fetch('http://' + config.ip + ':7777/start?height=' + config.flyHeight + '&duration=' + config.flyDuration, {
                    method: 'post'
                }).then(res => {
                    console.log(res);
                });

                this.run = !this.run;
                this.$emit('startDemo', this.run);


                // таймаут стрима
                /*setTimeout(() => {
                    this.run = !this.run;
                    this.$emit('startDemo', this.run);
                }, config.flyDuration * 1000)*/
            }
        }
    }
</script>

<style scoped>
    .start-border {
        position: relative;
        height: 600px;
        width: 840px;
        border: 5px solid #FFD100;
    }

    .start-border-lg {
        position: relative;
        height: 800px;
        width: 1199px;
        border: 8px solid #FFD100;
        margin-left: 100px;
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

    .horiz-crop-lg, .vert-crop-lg {
        position: absolute;
        background-color: #031323;
    }

    .horiz-crop-lg {
        top: 100px;
        left: -8px;
        height: 600px;
        width: 1215px;
    }

    .vert-crop-lg {
        top: -8px;
        left: 100px;
        height: 816px;
        width: 998px;
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

    .video-stream {
        background-color: aliceblue;
        z-index: 1000;
        height: 480px;
        width: 720px;
        position: absolute;
        /*background-color: red;*/
        top: 160px;
        left: 239px;
        transform: scale(1.666);
    }

    iframe {
        width: 720px;
        height: 480px;
    }
</style>