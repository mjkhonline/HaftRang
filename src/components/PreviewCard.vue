<template>
    <div class="row justify-content-center">
        <div class="col-12 col-md-8">
            <img ref="imgPreview" @load="updateImage" id="img-preview" alt="uploaded photo preview"
                 :src="imageURL"/>
        </div>
    </div>
</template>

<script>

    export default {
        name: "PreviewCard",
        props: {
            imageURL: {
                type: String,
                required: true
            }
        },
        data() {
            return {}
        },
        methods: {
            updateImage() {
                this.$emit('imageLoaded', this.$refs.imgPreview);
            }
        }
    }
</script>

<style lang="scss" scoped>
    img {
        border-radius: 3%;
        max-width: 100%;
        max-height: 50rem;
        margin: 0.3em auto;
        box-shadow: 0 0 40px grey;
    }
</style>