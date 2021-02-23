<template>
    <h1>paletten</h1>
    <div class="card">
        <Search @imageToDisplay="imageToDisplay" />
        <Palette :imageUrl="imageURL" />
    </div>
</template>

<script>
import Palette from '@/components/Palette'
import Search from '@/components/Search'

export default {
    components: {
        Palette,
        Search,
    },
    data() {
        return {
            imageURL: '',
        }
    },
    methods: {
        imageToDisplay(url) {
            this.imageURL = url
        },
    },
}
</script>

<style lang="scss">
:root {
    --color-primary: #333;
    --color-secondary: #333;
    --color-card: #fff6e2;
}

html {
    font-size: 62.5%;
    @media (max-width: 650px) {
        font-size: 50%;
    }
}

* {
    box-sizing: border-box;
    margin: 0;
}

body {
    font-family: Meiryo, sans-serif, monospace;
    background: var(--color-primary);
    max-width: 1925px;
    margin: 0 auto;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

h1 {
    color: var(--color-secondary);
    letter-spacing: 0.2rem;
    position: absolute;
    top: 5rem;
    left: 5rem;
}

.card {
    overflow: visible;
    width: 48rem;
    height: 55rem;
    padding: 3rem;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
        0 4px 6px -2px rgba(0, 0, 0, 0.05);
    background-color: var(--color-card);
    border-radius: 1rem;
}
</style>
