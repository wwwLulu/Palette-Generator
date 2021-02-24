<template>
    <div class="dots">
        <div class="dot"></div>
        <div class="dot"></div>
        <div class="dot"></div>
        <div class="dot"></div>
        <div class="dot"></div>
        <div class="dot"></div>
    </div>
</template>

<style lang="scss" scoped>
.dots {
    display: flex;
    margin-bottom: 2rem;
}
.dot {
    min-width: 1.2rem;
    min-height: 1.2rem;
    border-radius: 100%;
    margin: 1rem;
    background-image: linear-gradient(
        145deg,
        rgba(255, 255, 255, 0.5) 0%,
        rgba(0, 0, 0, 0) 100%
    );
    animation: bouncey 1.5s 0.5s linear infinite;
}
.dot:nth-child(1) {
    background-color: var(--color-0);
}

.dot:nth-child(2) {
    background-color: var(--color-1);
    animation-delay: 0.1s;
}

.dot:nth-child(3) {
    background-color: var(--color-2);
    animation-delay: 0.2s;
}

.dot:nth-child(4) {
    background-color: var(--color-3);
    animation-delay: 0.3s;
}

.dot:nth-child(5) {
    background-color: var(--color-4);
    animation-delay: 0.4s;
}

.dot:nth-child(6) {
    background-color: var(--color-5);
    animation-delay: 0.5s;
}

@keyframes bouncey {
    0%,
    50%,
    100% {
        transform: scale(1);
    }
    25% {
        transform: scale(0.6);
    }
    75% {
        transform: scale(1.4);
    }
}
</style>
