<template>
    <div class="row mt-2 pb-2 bg-dark text-white">
        <div class="col-12 p-4">
            <h2>Preferences</h2>
            <div class="row justify-content-center">
                <div class="col-12 col-md-10 col-lg-8">
                    <range-slider :value="palettesCount" :min-value=4 :max-value=20 :default-value=5>
                        Adjust number of palettes
                    </range-slider>
                </div>
            </div>

        </div>
    </div>

</template>

<script>
    import RangeSlider from "./Elements/RangeSlider";

    export default {
        name: "ControlCard",
        components: {RangeSlider},
        props: {
            palettesCount: {
                type: Number,
                required: true
            }
        },
        data() {
            return {
            }
        }
    }
</script>

<style scoped>

</style>