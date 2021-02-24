<template>
    <Loader v-show="searching" />
    <form v-show="!searching" action="#">
        <input v-model="query" type="text" placeholder="what's your vibe" />
        <button @click="getImage">palette</button>
    </form>
</template>

<script>
import config from '@/config.json'
import Loader from '@/components/Loader.vue'

export default {
    props: ['searching'],
    emits: ['loaderEnabled'],
    components: {
        Loader,
    },
    emits: ['imageToDisplay', 'loaderEnabled'],
    data() {
        return {
            query: '',
            image: '',
        }
    },
    methods: {
        async getImage() {
            this.$emit('loaderEnabled')
            var API_KEY = process.env.apikey || config.API_KEY
            var URL =
                'https://pixabay.com/api/?key=' +
                API_KEY +
                '&q=' +
                encodeURIComponent(this.query) +
                '&image_type=photo'
            try {
                const data = await fetch(URL)
                const res = await data.json()

                //Get random image
                let imageNum = Math.floor(Math.random() * res.hits.length)
                this.image = res.hits[imageNum].largeImageURL
                this.$emit('imageToDisplay', this.image)
            } catch (e) {
                console.log(e)
            }
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
