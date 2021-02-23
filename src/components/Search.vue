<template>
    <form action="#">
        <input
            v-model="imageUrl"
            type="text"
            placeholder="Share the image path!"
        />
        <button @click="getPaletteFromURL">Get Palette</button>
    </form>
</template>

<script>
export default {
    emits: ['imageToDisplay'],
    data() {
        return {
            imageUrl: '',
        }
    },
    methods: {
        getPaletteFromURL() {
            this.$emit('imageToDisplay', this.imageUrl)
        },
    },
}
</script>

<style scoped lang="scss">
button {
    cursor: pointer;
    font-weight: bold;
    font-size: 1.4rem;
    border-radius: 1rem;
    background: darken(#fff6e2, 20);
    margin-left: 0.5rem;
    padding: 1.4rem 1.6rem;
    border: none;
}

input {
    letter-spacing: 0.1rem;
    border-radius: 1rem;
    padding-left: 1.5rem;
    font-size: 1.6rem;
    font-weight: thin;
    height: 4.5rem;
    min-width: 30rem;
    margin-bottom: 2rem;
    // color: darken(#fff6e2, 50);

    &::placeholder {
        color: darken(#fff6e2, 50);
    }
    border: none;
    border: solid 1px black;
    // border-color: darken(#fff6e2, 10);
    outline: none;
}
</style>
