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
    z-index: 5000;
    width: 100%;
    display: flex;
    justify-content: space-between;
}

button {
    z-index: 4000;
    position: relative;
    &::before {
        z-index: 3000;
        content: '';
        position: absolute;
        width: 100%;
        height: 100%;
        top: 0.2rem;
        left: 0.2rem;
        border: 1px solid black;
        opacity: 0.5;
        border-radius: 1rem;
    }
    border: 1px solid black;
    cursor: pointer;
    font-weight: bold;
    font-size: 1.8rem;
    border-radius: 1rem;
    // background: darken(#fff6e2, 20);
    background: #f0f0f0;
    margin-left: 0.5rem;
    height: 4.5rem;
    padding: 1rem 1.8rem;
    &:hover {
        animation: Bounce 0.5s linear;
    }
}

input {
    color: white;
    // background: var(--color-secondary);
    letter-spacing: 0.1rem;
    border-radius: 1rem;
    padding-left: 1.5rem;
    font-size: 1.6rem;
    font-weight: thin;
    height: 4.5rem;
    min-width: 30rem;
    margin-bottom: 2rem;
    color: black;
    &:active {
        animation: Bounce 0.2s linear;
    }
    &::placeholder {
        color: darken(#fff6e2, 70);
    }
    border: none;
    border: solid 1px black;
    outline: none;
}
</style>
