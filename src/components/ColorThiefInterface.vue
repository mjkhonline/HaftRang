<script>
    import ColorThief from "colorthief"

    const ct = new ColorThief();
    export default {
        name: "ColorThiefInterface",
        methods: {
            getPalettes(imageElement, palettesCount, sampleSkip = 10, outputFormat = 'hex') {
                if (imageElement.complete) {
                    const palettes = ct.getPalette(imageElement, palettesCount, sampleSkip);
                    switch (outputFormat) {
                        case 'rgb':
                            return palettes.map(this.arrayToRGB);
                        case 'array':
                            return palettes;
                        default:
                            return palettes.map(this.arrayToHex);
                    }
                }
                return [];
            },
            arrayToHex(arr) {
                let out = '#';
                for (let i = 0; i < 3; i++)
                    out += arr[i].toString(16);
                return out;
            },
            arrayToRGB(arr) {
                return `rgb(${arr[0]},${arr[1]},${arr[2]})`;
            }
        }
    }
</script>