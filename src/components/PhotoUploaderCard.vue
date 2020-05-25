<template>
    <div class="row justify-content-center mb-5">
        <div class="col-12 col-md-7">
            <div id="uploadBox" class="d-flex flex-column justify-content-center text-center" ref="dragArea"
                 @dragover.stop.prevent="dragOver" @drop.stop.prevent="dropFile" @dragleave="dragLeave">
                <h2>{{dragMsg}}</h2>
                <p>drag and drop your photos here</p>
                <button :style="{visibility: isDragOver ? 'hidden' : 'visible'}" @click="selectImageDialogBox"
                        class="btn btn-info d-inline align-self-center">Browse
                </button>
                <input ref="imageInput" @input="onImageSelected" type="file" class="d-none"
                       accept="image/png, .jpeg, .jpg, image/gif"/>
            </div>
        </div>
    </div>
</template>

<script>
    const reader = new FileReader;

    export default {
        name: "PhotoUploaderCard",
        data() {
            return {
                inputURL: null,
                isDragOver: false
            }
        },
        methods: {
            selectImageDialogBox() {
                this.$refs.imageInput.click();
            },
            onImageSelected() {
                const files = this.$refs.imageInput.files;
                if (files && files[0]) {
                    reader.onload = e => {
                        this.inputURL = e.target.result
                        this.$emit('input', this.inputURL);
                    };
                    reader.readAsDataURL(files[0]);
                }
            },
            dragOver(event) {
                event.dataTransfer.dropEffect = 'copy';
                this.isDragOver = true;
                this.$refs.dragArea.style.backgroundColor = '#333'
                this.$refs.dragArea.style.color = '#efefef'
            },
            dropFile(event) {
                const files = event.dataTransfer.files;
                if (files && files[0]) {
                    reader.onload = e => {
                        this.inputURL = e.target.result
                        this.$emit('input', this.inputURL);
                    };
                    reader.readAsDataURL(files[0]);
                }
                this.isDragOver = false;
                this.$refs.dragArea.style.backgroundColor = 'white'
                this.$refs.dragArea.style.color = 'black'
            },
            dragLeave() {
                this.isDragOver = false;
                this.$refs.dragArea.style.backgroundColor = 'white'
                this.$refs.dragArea.style.color = 'black'
            }
        },
        computed: {
            dragMsg() {
                return this.isDragOver ? 'Release...' : 'Upload Box';
            }
        }
    }
</script>

<style lang="scss" scoped>
    #uploadBox {
        width: 100%;
        height: 12em;
        box-shadow: 0 0 10px rgba(136, 136, 136, 0.85);
        transition: all 220ms ease-out;

        &:hover {
            box-shadow: 0 0 20px rgba(136, 136, 136);
        }
    }

    #uploadBoxCover {
        background-color: #333;
        width: 100%;
        height: 100%;
        position: absolute;
        color: white;
    }
</style>