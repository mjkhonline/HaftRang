<template>
    <div class="slider-container">
        <div class="range-slider">
            <span class="rs-label">{{value}}</span>
            <input class="rs-range" type="range" title="adjust number of palettes to extract"
                   :value="value" @input="updatePalettesCount($event.target.value)" :min="minValue" :max="maxValue">
        </div>
        <div class="box-minmax">
            <span>{{minValue}}</span><span>{{maxValue}}</span>
        </div>
        <slot></slot>
    </div>
</template>

<script>
    import {eventBus} from "../../main";

    export default {
        name: "RangeSlider",
        props: {
            value: {
                type: Number,
                required: true
            },
            minValue: {
                type: Number,
                required: true
            },
            maxValue: {
                type: Number,
                required: true
            },
            defaultValue: {
                type: Number,
                required: false,
            }
        },
        data() {
            return {}
        },
        methods: {
            updatePalettesCount(newVal) {
                eventBus.$emit('palettesCountUpdated', newVal);
            }
        },
        computed: {}

    }


</script>

<style lang="scss" scoped>
    @import "../../assets/sass/colors";

    .slider-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    .box-minmax {
        margin-top: 1em;
        width: 100%;
        display: flex;
        justify-content: space-between;
    }

    .range-slider {
        width: 100%;
    }

    .rs-range {
        margin-top: 2em;
        width: 100%;
        -webkit-appearance: none;

        &:focus {
            outline: none;
        }

        &::-webkit-slider-runnable-track {
            width: 100%;
            height: 4px;
            cursor: pointer;
            box-shadow: none;
            background: #ffffff;
            border-radius: 0;
            border: 0 solid #010101;
        }

        &::-moz-range-track {
            width: 100%;
            height: 4px;
            cursor: pointer;
            box-shadow: none;
            background: #ffffff;
            border-radius: 0;
            border: 0 solid #010101;
        }

        &::-webkit-slider-thumb {
            border: 0 solid #ffffff;
            box-shadow: 0 10px 10px rgba(0, 0, 0, 0.25);
            height: 42px;
            width: 22px;
            border-radius: 22px;
            background: $c-warning;
            cursor: pointer;
            -webkit-appearance: none;
            margin-top: -20px;
        }

        &::-moz-range-thumb {
            border: 0 solid #ffffff;
            box-shadow: 0 10px 10px rgba(0, 0, 0, 0.25);
            height: 42px;
            width: 22px;
            border-radius: 22px;
            background: $c-warning;
            cursor: pointer;
            -webkit-appearance: none;
            margin-top: -20px;
        }

        &::-moz-focus-outer {
            border: 0;
        }
    }

    .rs-label {
        position: absolute;
        right: 0.5em;
        top: -2em;
        display: block;
        width: 60px;
        height: 60px;
        text-align: center;
        background: $c-warning;
        padding: 0.2em;
        border: 1px solid #fff;
        color: black;
        font-size: 1.8em;
    }
</style>