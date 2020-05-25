<template>
    <div id="app">
        <header-card></header-card>
        <photo-uploader-card v-model="imageURL"></photo-uploader-card>
        <preview-card v-if="imageURL" @imageLoaded="updateImage" :imageURL="imageURL"></preview-card>
        <palettes-card :palettes="palettes"></palettes-card>
        <control-card v-if="imageURL" :palettesCount="palettesCount"></control-card>
    </div>
</template>

<script>

    import HeaderCard from "./components/HeaderCard";
    import PreviewCard from "./components/PreviewCard";
    import PalettesCard from "./components/PalettesCard";
    import cti from "./components/ColorThiefInterface";
    import ControlCard from "./components/ControlCard";
    import {eventBus} from './main';
    import PhotoUploaderCard from "./components/PhotoUploaderCard";
    import VueScrollTo from 'vue-scrollto';

    export default {
        name: 'App',
        data() {
            return {
                imageSource: null,
                imageURL: null,
                palettesCount: 5,
                palettes: []
            }
        },
        methods: {
            updateImage(img) {
                this.imageSource = img;
                this.getPalettes();
            },
            updatePalettesCount(newValue) {
                this.palettesCount = parseInt(newValue);
                this.getPalettes();
            },
            getPalettes() {
                if (this.imageSource) {
                    this.palettes = cti.methods.getPalettes(this.imageSource, this.palettesCount);
                    VueScrollTo.scrollTo('#palettesCard', 1000, {'easing': 'ease-in-out','force':false});
                } else
                    this.palettes = [];
            }
        },

        computed: {},
        components: {
            PhotoUploaderCard,
            ControlCard,
            ColorThiefInterface: cti,
            PalettesCard,
            PreviewCard,
            HeaderCard
        },
        created() {
            eventBus.$on('palettesCountUpdated', this.updatePalettesCount);
        }
    }
</script>

<style lang="scss">
    @import "./assets/sass/base";
</style>
