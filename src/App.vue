<template>
    <div id="app">
        <header-card></header-card>
        <transition name="fade" type="transition" appear>
            <photo-uploader-card v-model="imageURL"></photo-uploader-card>
        </transition>
        <transition name="fade" type="transition">
            <preview-card v-if="imageURL" @imageLoaded="updateImage" :imageURL="imageURL"></preview-card>
        </transition>
        <palettes-card :palettes="palettes"></palettes-card>
        <control-card v-if="imageURL" :palettesCount="palettesCount"></control-card>
        <footer-card></footer-card>
    </div>
</template>

<script>

    import HeaderCard from "./components/HeaderCard";
    import FooterCard from "./components/FooterCard";
    import PreviewCard from "./components/PreviewCard";
    import PalettesCard from "./components/PalettesCard";
    import cti from "./components/ColorThiefInterface";
    import ControlCard from "./components/ControlCard";
    import {eventBus} from './main';
    import PhotoUploaderCard from "./components/PhotoUploaderCard";
    import VueScrollTo from 'vue-scrollto';
    import axios from 'axios';

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
                axios.put('/palettes/count.json',this.palettesCount).then(
                    response => console.log(response)
                ).catch(e => console.log(e));
            },
            getPalettes() {
                if (this.imageSource) {
                    this.palettes = cti.methods.getPalettes(this.imageSource, this.palettesCount);
                    VueScrollTo.scrollTo('#palettesCard', 1000, {'easing': 'ease-in-out', 'force': false});
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
            HeaderCard,
            FooterCard
        },
        created() {
            eventBus.$on('palettesCountUpdated', this.updatePalettesCount);
            axios.get('/palettes/count.json').then(
                response => this.palettesCount = response.data
            ).catch(e => console.log(e));
        }
    }
</script>

<style lang="scss">
    @import "./assets/sass/base";

    .fade-enter {
        opacity: 0;
    }

    .fade-enter-active {
        transition: opacity 700ms;
    }

    .fade-leave {

    }

    .fade-leave-active {
        transition: opacity 500ms;
        opacity: 0;
    }
</style>
