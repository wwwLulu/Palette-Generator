<template>
    <div class="card">
        <form action="#">
            <input type="text" />
            <button>Get Palette</button>
        </form>
        <Palette />
    </div>
</template>

//
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
    margin-left: 1rem;
    padding: 1.5rem 2rem;
    border: none;
}

input {
    padding-left: 0.5rem;
    font-size: 1.4rem;
    font-weight: bold;
    height: 4rem;
    min-width: 30rem;
    margin-bottom: 2rem;
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
