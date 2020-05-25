<template>
    <div class="row justify-content-center my-5" v-show="palettes" id="palettesCard">
        <div v-for="color in palettes" class="col color-preview" :style="{backgroundColor: color}">
            <p>{{color | capitalize}}</p>
        </div>
    </div>
</template>

<script>
    export default {
        name: "PalettesCard",
        props: {
            palettes: {
                type: Array,
                required: false,
                default: () => [],
            }
        },
        filters: {
            capitalize(value) {
                return value.toUpperCase();
            }
        }
    }
</script>

<style lang="scss" scoped>
    .color-preview {
        height: 8em;
        margin: 0;

        p {
            text-align: center;
            position: relative;
            top: 3.3em;
            text-shadow: 0 0 10px #bbb;
        }
    }
</style>