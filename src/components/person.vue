<template>
    <div class="flex-container-column person-wrap">
        <div class="persons">
            <div class="person" v-for="person in detectedPersons">
                <div class="person-photo">
                    <img :src="person.imgURL" alt="photo">
                </div>
                <div class="person-data">
                    <div class="data-field">
                        <span class="key">Фамилия</span> <br>
                        <span class="value">{{person.lastName}}</span>
                    </div>
                    <div class="data-field">
                        <span class="key">Имя</span> <br>
                        <span class="value">{{person.name}}</span>
                    </div>
                    <div class="data-field">
                        <span class="key">Отчество</span> <br>
                        <span class="value">{{person.midName}}</span>
                    </div>
                </div>
            </div>
        </div>
        <div class="stop-stream">
            <button class="stop" @click="stopStream">ЗАКОНЧИТЬ</button>
        </div>
    </div>
</template>

<script>
    import {config} from "../dron-config";

    export default {
        name: "person",
        data: function () {
            return {
                socket: null,
                stompClient: null,
                detectedPersons: []
            }
        },
        methods: {
            stopStream() {
                window.fetch('http://' + config.ip + ':7777/stop', {
                    method: 'post'
                }).then(res => {
                    console.log(res);
                });
            }
        },
        created() {
            this.socket = new SockJS('http://localhost:9000/stomp');
            this.stompClient = Stomp.over(this.socket);

            this.stompClient.connect({}, () => {
                this.stompClient.subscribe('/topic/message', (data) => {

                    let parsedArray = JSON.parse(data.body);
                    parsedArray.forEach((person) => {
                        this.detectedPersons.push(JSON.parse(person.userData));
                    });
                })
            })
        },
        destroyed() {
            this.stompClient.unsubscribe();
            this.stompClient.disconnect();
        }
    }
</script>

<style scoped>

    img {
        width: 100%;
    }


    .person-wrap {
        margin-left: 80px;
        height: 816px;
        width: 460px;
    }

    .persons {
        height: 716px;
        width: 100%;
        overflow: hidden;
        overflow-y: scroll;
        border: 1px solid #57A1D0;
        border-top: 4px solid #57A1D0;
        background-color: #0D2C49;
    }

    .person {
        clear: both;
        width: 460px;
    }

    .person-photo, .person-data {
        float: left;
        box-sizing: border-box;
        width: 50%;
    }

    .person-data > div {
        padding: 8px;
    }

    .data-field {
    }

    .key {
        font-size: 14px;
    }
    .value {
        font-size: 18px;
        color: #FED101;
    }
    .stop-stream {
        height: 100px;
        width: 100%;
    }

    /* width */
    ::-webkit-scrollbar {
        width: 4px;
    }

    /* Track */
    ::-webkit-scrollbar-track {
        box-shadow: inset 0 0 4px grey;
        margin: 4px 0;
        /*border-radius: 10px;*/
    }

    /* Handle */
    ::-webkit-scrollbar-thumb {
        background: #57A1D0;
        border-radius: 0px;
    }

    .stop {
        font-size: 40px;
        font-family: Bender-Black, sans-serif;
        width: 100.5%;
        height: 100%;
        border: 10px solid white;
        background-color: #FFD100;
        cursor: pointer;
    }

</style>