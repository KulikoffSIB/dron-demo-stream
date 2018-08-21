<template>
    <div class="person-wrap">
        <div class="flex-container-column">
            <div class="flex-element-6">
                <div class="flex-container-column">
                    <div class="flex-element-3 photo">
                        PHOTO FIO
                    </div>
                    <div class="flex-element-2 user-data">
                        USER DATA
                    </div>
                    <div class="flex-element-1 event">
                        EVENT
                    </div>
                </div>
            </div>
            <div class="flex-element-2">LOGO | LOGO</div>
        </div>
        Данные пользователя
    </div>
</template>

<script>
    export default {
        name: "person",
        data: function () {
            return {

            }
        }
    }
</script>

<style scoped>
    .person-wrap {
        margin-left: 40px;
        width: 400px;
        height: 813px;
        border: 1px solid #57A1D0;
        border-top: 4px solid #57A1D0;
    }

    .border-warning {
        border-color: #cd0000;
    }

    .border-ok {
        border-color: #76bf2c;
    }
</style>