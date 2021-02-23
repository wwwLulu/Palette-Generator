<template>
    <form action="#">
        <input v-model="imageUrl" type="text" placeholder="Share image URL!" />
        <button @click="getPaletteFromURL">palette</button>
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
form {
    width: 100%;
    display: flex;
    justify-content: space-between;
}

button {
    border: 1px solid black;
    cursor: pointer;
    font-weight: bold;
    font-size: 1.8rem;
    border-radius: 1rem;
    // background: darken(#fff6e2, 20);
    color: var(--color-primary);
    background: var(--color-secondary);
    margin-left: 0.5rem;
    height: 4.5rem;
    padding: 1rem 1.8rem;
}

input {
    background: var(--color-secondary);
    letter-spacing: 0.1rem;
    border-radius: 1rem;
    padding-left: 1.5rem;
    font-size: 1.6rem;
    font-weight: thin;
    height: 4.5rem;
    min-width: 30rem;
    margin-bottom: 2rem;
    color: var(--color-primary);

    // color: darken(#fff6e2, 50);

    &::placeholder {
        // color: darken(#fff6e2, 50);
        color: var(--color-primary);
    }
    border: none;
    border: solid 1px black;
    // border-color: darken(#fff6e2, 10);
    outline: none;
}
</style>
