<template>
    <div class="card">
        <form action="#">
            <input type="text" placeholder="Whats the Vibe?" />
            <button>Get Palette</button>
        </form>
        <Palette />
    </div>
</template>

<script>
import Palette from '@/components/Palette'
export default {
    components: {
        Palette,
    },
}
</script>

<style lang="scss">
:root {
    --color-primary: #333;
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
