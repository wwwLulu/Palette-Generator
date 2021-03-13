<template>
    <section class="image-info">
        <div class="img__container" ref="imgContainer">
            <img
                class="backdrop"
                :src="
                    imageUrl ? googleProxy + imageUrl : googleProxy + imageURL
                "
                crossorigin="anonymous"
                ref="img"
                alt=""
            />
            <img
                @load="generatePalette"
                class="img"
                :src="
                    imageUrl ? googleProxy + imageUrl : googleProxy + imageURL
                "
                crossorigin="anonymous"
                ref="img"
                alt=""
            />
        </div>
        <div class="blocks">
            <div @click="copyToClipboard" class="block">
                <p class="block__hex"></p>
            </div>
            <div @click="copyToClipboard" class="block">
                <p class="block__hex"></p>
            </div>
            <div @click="copyToClipboard" class="block">
                <p class="block__hex"></p>
            </div>
            <div @click="copyToClipboard" class="block">
                <p class="block__hex"></p>
            </div>
            <div @click="copyToClipboard" class="block">
                <p class="block__hex"></p>
            </div>
            <div @click="copyToClipboard" class="block">
                <p class="block__hex"></p>
            </div>
        </div>
    </section>
</template>

<script>
import ColorThief from 'colorthief'

export default {
    props: ['imageUrl'],
    emits: ['loaderDisabled'],
    data() {
        return {
            imageURL:
                'https://images.pexels.com/photos/1098520/pexels-photo-1098520.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260',
            googleProxy:
                'https://images1-focus-opensocial.googleusercontent.com/gadgets/proxy?container=focus&refresh=2592000&url=',
        }
    },
    methods: {
        copyToClipboard() {},
        convertToHex(color) {
            let hex = color.toString(16)
            return hex.length == 1 ? '0' + hex : hex
        },
        rgbToHex(r, g, b) {
            return (
                '#' +
                this.convertToHex(r) +
                this.convertToHex(g) +
                this.convertToHex(b)
            )
        },
        invertColor(hex) {
            if (hex.indexOf('#') === 0) {
                hex = hex.slice(1)
            }
            // convert 3-digit hex to 6-digits.
            if (hex.length === 3) {
                hex = hex[0] + hex[0] + hex[1] + hex[1] + hex[2] + hex[2]
            }
            if (hex.length !== 6) {
                throw new Error('Invalid HEX color.')
            }
            // invert color components
            let r = (255 - parseInt(hex.slice(0, 2), 16)).toString(16),
                g = (255 - parseInt(hex.slice(2, 4), 16)).toString(16),
                b = (255 - parseInt(hex.slice(4, 6), 16)).toString(16)
            // pad each with zeros and return
            return '#' + this.padZero(r) + this.padZero(g) + this.padZero(b)
        },
        padZero(str, len) {
            len = len || 2
            let zeros = new Array(len).join('0')
            return (zeros + str).slice(-len)
        },
        generatePalette() {
            this.$emit('loaderDisabled')
            try {
                const img = document.querySelector('img')
                const blocks = document.querySelectorAll('.block')
                const colorThief = new ColorThief()
                const palette = colorThief.getPalette(img)

                //Set Background to images dominant color
                document.documentElement.style.setProperty(
                    '--color-primary',
                    `rgb(${palette[0][0]},${palette[0][1]},${palette[0][2]})`
                )

                for (let i = 0; i < blocks.length; i++) {
                    blocks[
                        i
                    ].style.backgroundColor = `rgb(${palette[i][0]},${palette[i][1]},${palette[i][2]})`

                    let hexColor = this.rgbToHex(
                        palette[i][0],
                        palette[i][1],
                        palette[i][2]
                    )
                    //Convert RGB values to HEX for display
                    blocks[i].firstChild.innerHTML = hexColor
                    blocks[i].firstChild.style.color = this.invertColor(
                        hexColor
                    )
                    if (i == 0) {
                        document.documentElement.style.setProperty(
                            '--color-secondary',
                            this.invertColor(hexColor)
                        )
                    }
                    switch (i) {
                        case 0:
                            document.documentElement.style.setProperty(
                                '--color-0',
                                hexColor
                            )
                            break
                        case 1:
                            document.documentElement.style.setProperty(
                                '--color-1',
                                hexColor
                            )
                            break
                        case 2:
                            document.documentElement.style.setProperty(
                                '--color-2',
                                hexColor
                            )
                            break
                        case 3:
                            document.documentElement.style.setProperty(
                                '--color-3',
                                hexColor
                            )
                            break
                        case 4:
                            document.documentElement.style.setProperty(
                                '--color-4',
                                hexColor
                            )
                            break
                        case 5:
                            document.documentElement.style.setProperty(
                                '--color-5',
                                hexColor
                            )
                            break
                    }
                }
            } catch (e) {
                console.log(e)
            }
        },
    },
}
</script>
<style scoped lang="scss">
.blocks {
    position: absolute;
    right: 0rem;
    height: 40rem;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    &:hover .block__hex {
        opacity: 1;
    }
}

.block {
    display: block;
    width: 8.5rem;
    height: 6rem;
    display: flex;
    justify-content: center;
    align-items: center;
    font-weight: bold;
    font-size: 1.2rem;
    &__hex {
        transition: all 0.3s;
        opacity: 0;
    }
}

.img__container {
    &:hover {
        transform: scale(1.05);
    }
    z-index: 500;
    position: relative;
    min-width: 40rem;
    min-height: 40rem;
    max-width: 40rem;
    max-height: 40rem;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
        0 4px 6px -2px rgba(0, 0, 0, 0.05);
    border-radius: 1rem;
    animation: fall-bound 1s cubic-bezier(0.94, 0.01, 1, 1) 0.15s forwards;
    transition: all 0.3s ease-out;

    .backdrop {
        z-index: 1000;
        position: absolute;
        top: 2rem;
        opacity: 0.5;
        filter: blur(8px);
    }
    img {
        position: absolute;
        z-index: 2000;
        border-radius: inherit;
        width: 100%;
        height: 100%;
        object-fit: cover;
        object-position: top;
    }
}

.image-info {
    position: relative;
    display: flex;
    justify-content: space-between;
    margin-left: -9rem;
}
</style>
