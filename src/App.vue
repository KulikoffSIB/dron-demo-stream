<template>
    <div id="app">
        <div class="flex-container-row flex-align-vert-center">
            <div class="flex-element-1">
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
                <start></start>
            </div>
        </div>
    </div>
</template>

<script>
    import Start from "./components/start";

    export default {
        name: 'App',
        components: {Start}
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
