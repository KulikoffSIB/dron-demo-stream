<template>
    <div id="app">
        <div class="flex-container-row flex-align-vert-center">

            <div class="flex-element-1" v-if="!run">
                <div class="logo-wrap">
                    <div class="logo rosneft">
                        <img src="../src/assets/RN.png" alt="ROSNEFT">
                    </div>
                    <div class="logo sibintek">
                        <img src="../src/assets/SIB.png" alt="SIBINTEK">
                    </div>
                </div>
            </div>
            <div class="flex-element-1">
                <start @startDemo="startDemo"></start>
            </div>
            <div class="flex-element-1" v-if="run" style="align-self: center;">
                <person></person>
            </div>
        </div>
    </div>
</template>

<script>
    import Start from "./components/start";
    import Person from "./components/person";

    export default {
        name: 'App',
        components: {Person, Start},
        data: function () {
            return {
                run: false
            }
        },
        methods: {
            startDemo: function (run) {
                this.run = run;
            }
        },
        computed: {}
    }
</script>

<style>
    #app {
        height: 100%;
    }

    .logo-wrap {
        margin-left: 100px;
    }

    .logo {
        display: table-cell;
        height: 260px;
        vertical-align: middle;
    }

    .rosneft, .sibintek {

    }

    .rosneft {
        padding-right: 30px;
    }

    .sibintek {
        padding-left: 50px;
        padding-top: 30px;
        border-left: 1px solid #CBCDCF;
    }

</style>
