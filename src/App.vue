<template>
    <h1>paletten</h1>
    <div class="card">
        <Search @imageToDisplay="imageToDisplay" />
        <Palette :imageUrl="imageURL" />
    </div>
    <Info />
</template>

<script>
import Palette from '@/components/Palette'
import Search from '@/components/Search'
import Info from '@/components/Info'

export default {
    components: {
        Palette,
        Search,
        Info,
    },
    data() {
        return {
            imageURL: '',
        }
    },
    watch: {
        imageURL() {
            setTimeout(() => {
                document
                    .querySelector('.img__container')
                    .classList.add('bounce')
            }, 0)
            setTimeout(() => {
                document
                    .querySelector('.img__container')
                    .classList.remove('bounce')
            }, 3000)
        },
    },
    methods: {
        imageToDisplay(url) {
            this.imageURL = url
        },
    },
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Alatsi&family=Capriola&display=swap');
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
    font-family: 'Alatsi', sans-serif;
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

.bounce {
    transition: all 0.5s;
    animation: fall-bound 1s cubic-bezier(0.94, 0.01, 1, 1) 0.15s forwards;
}

@keyframes Bounce {
    10% {
        transform: scale(0.96);
    }
    50% {
        transform: scale(1.04);
    }
    100% {
        transform: scale(1);
    }
}

@keyframes fall-bound {
    0% {
        transform: translateY(-200%) scaleX(1) scaleY(1);
        opacity: 0;
    }
    40% {
        transform: translateY(0%) scaleX(1.6) scaleY(0.8);
        opacity: 1;
    }
    50% {
        transform: translateY(-6%) scaleX(1) scaleY(1);
        opacity: 1;
    }
    60% {
        transform: translateY(0%) scaleX(1.3) scaleY(0.9);
        opacity: 1;
    }
    70% {
        transform: translateY(-3%) scaleX(1) scaleY(1);
        opacity: 1;
    }
    80% {
        transform: translateY(0%) scaleX(1.15) scaleY(0.95);
        opacity: 1;
    }
    90% {
        transform: translateY(-1.5%) scaleX(1) scaleY(1);
        opacity: 1;
    }
    100% {
        transform: translateY(0%) scaleX(1) scaleY(1);
        opacity: 1;
    }
}
</style>
