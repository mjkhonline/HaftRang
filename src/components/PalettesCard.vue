<template>
    <transition-group v-show="palettes" name="color-preview" tag="div" class="row justify-content-center my-5"
                      id="palettesCard">
        <div v-for="color in palettes" :key="color" class="col color-preview" :style="{backgroundColor: color}">
            <p>{{color | capitalize}}</p>
        </div>
    </transition-group>
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
        transition: all 1s; // for animation

        p {
            text-align: center;
            position: relative;
            top: 3.3em;
            text-shadow: 0 0 10px #bbb;
            color: black;
        }
    }

    .color-preview-enter, .color-preview-leave-to {
        opacity: 0;
        transform: translateX(30px);
    }

    .color-preview-leave-active {
        position: absolute;
    }


</style>