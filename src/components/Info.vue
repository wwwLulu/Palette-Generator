<template>
    <i @click="open = true" v-show="!open" class="fas fa-info"></i>
    <div class="info" v-show="open">
        <i @click="open = false" class="fas fa-times"></i>
        <p>
            Made entirely with Vue.js & Palette generated using ColorThief
            library
        </p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            open: false,
        }
    },
}
</script>

<style scoped>
.info p {
    max-width: 25rem;
    line-height: 2 rem;
    position: absolute;
    bottom: 8rem;
    right: 8rem;
    font-size: 1.6rem;
    color: var(--color-secondary);
}

i {
    cursor: pointer;
    position: absolute;
    font-size: 2rem;
    color: var(--color-primary);
    bottom: 2rem;
    right: 2rem;
    background: var(--color-secondary);

    border-radius: 50%;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
        0 4px 6px -2px rgba(0, 0, 0, 0.05);
}

.fa-info {
    padding: 1.5rem 2.1rem;
}
.fa-times {
    padding: 1.5rem 1.7rem;
}
</style>
