<template>
    <div class="row justify-content-center my-5">
        <div class="d-flex flex-row justify-content-center col-12">
            <img id="header-icon" src="../assets/imgs/icon.svg" alt="App Icon"/>
            <div>
                <h1>
                    7Rang <small>Color Palettes</small>
                </h1>
                <p>the combination of computer science and art</p>
            </div>
        </div>

    </div>

</template>

<script>
    export default {
        name: "HeaderCard",
        data() {
            return {}
        },
        methods: {}
    }
</script>

<style lang="scss" scoped>

    #header-icon {
        max-width: 85px;
        max-height: 85px;
        margin-right: 0.3em;

    }
</style>