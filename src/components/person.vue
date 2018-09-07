<template>
    <div class="person-logo-wrap">
        <div class="person-wrap">
            <div class="flex-container-column" style="height: 100%">
                <div class="flex-element-3">
                    <div class="flex-container-row">
                        <div class="flex-element-1">
                            <img src="" alt="" ref="photo">
                        </div>
                        <div class="flex-element-1">
                            <div class="flex-container-column">
                                <div class="flex-element-1 fio">
                                    <span class="key">Фамилия</span> <br>
                                    <span class="value">{{lastName}}</span>
                                </div>
                                <div class="flex-element-1 fio">
                                    <span class="key">Имя</span> <br>
                                    <span class="value">{{name}}</span>
                                </div>
                                <div class="flex-element-1 fio">
                                    <span class="key">Отчество</span> <br>
                                    <span class="value">{{midName}}</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="flex-element-1 user-data">
                    <div class="flex-container-row" style="height: 100%">
                        <div class="flex-element-1 fio">
                            <span class="key">Компания</span> <br>
                            <span class="value">{{company}}</span>
                        </div>
                        <div class="flex-element-1 fio">
                            <span class="key">Должность</span> <br>
                            <span class="value">{{post}}</span>
                        </div>
                    </div>
                </div>
                <!--<div v-bind:class="['flex-element-1', 'event', {ok: inHelmet != null && inHelmet}, {warning: inHelmet != null && !inHelmet}]">
                    <span v-if="inHelmet == null">Проверка наличия каски...</span>
                    <div v-else>
                        <div class="helmet-status" v-if="inHelmet">В каске</div>
                        <div class="helmet-status" v-else>Без каски</div>
                    </div>
                </div>-->
            </div>
        </div>
        <div class="logo-wrap">
            <div>

            </div>
        </div>
    </div>

</template>

<script>
    export default {
        name: "person",
        data: function () {
            return {
                inHelmet: null,
                name: 'Нет данных',
                lastName: 'Нет данных',
                midName: 'Нет данных',
                company: 'Нет данных',
                post: 'Нет данных',
                socket: null,
                stompClient: null,

            }
        },
        created() {
            this.socket = new SockJS('http://localhost:9000/stomp');
            this.stompClient = Stomp.over(this.socket);

            this.stompClient.connect({}, () => {
                this.stompClient.subscribe('/topic/message', (data) => {

                    let parsedArray = JSON.parse(data.body);
                    parsedArray.forEach((person)=>{
                        console.log(JSON.parse(person.userData))
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

    .person-logo-wrap {
        width: 402px;
        margin-left: 150px;
    }

    .person-wrap {
        margin-left: 40px;
        width: 400px;
        border: 1px solid #57A1D0;
        border-top: 4px solid #57A1D0;
        background-color: #0D2C49;
    }

    .logo-wrap {
        height: 200px;
        margin-left: 40px;
        margin-top: 268px;
        margin-right: 40px;
    }

    .logo {
        height: 160px
    }

    .ok {
        background-color: green;
    }

    .warning {
        background-color: red;
    }

    .border-warning {
        border-color: #cd0000;
    }

    .border-ok {
        border-color: #76bf2c;
    }

    .fio {
        padding: 20px;
    }

    .key {
        font-size: 16px;
    }

    .value {
        color: #FFD100;
        font-size: 20px;
        font-family: 'Bender-Bold', sans-serif;
    }

    .user-data {
        border-top: 1px solid #57A1D0;
    }
    .helmet-status, .event {
        text-align: center;
        font-size: 40px;
        padding-top: 20px;
        font-family: 'Bender-Bold', sans-serif;
    }

    .event {
        border-top: 1px solid #57A1D0;
        padding-top: 0;
    }
</style>