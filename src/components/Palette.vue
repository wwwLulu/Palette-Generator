<template>
    <section class="image-info">
        <div class="img__container">
            <img
                @load="generatePalette"
                class="img"
                :src="googleProxy + imageURL"
                crossorigin="anonymous"
                ref="img"
                alt=""
            />
        </div>
        <div class="blocks">
            <div class="block"><p class="block__hex"></p></div>
            <div class="block"><p class="block__hex"></p></div>
            <div class="block"><p class="block__hex"></p></div>
            <div class="block"><p class="block__hex"></p></div>
            <div class="block"><p class="block__hex"></p></div>
            <div class="block"><p class="block__hex"></p></div>
        </div>
    </section>
</template>

<script>
import ColorThief from 'colorthief'

export default {
    data() {
        return {
            imageURL:
                'https://i.pinimg.com/originals/34/09/2a/34092a9f367cc25e2b3ddd222aedcb07.jpg',
            googleProxy:
                'https://images1-focus-opensocial.googleusercontent.com/gadgets/proxy?container=focus&refresh=2592000&url=',
        }
    },
    methods: {
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
    margin-left: 3rem;
    height: 40rem;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    &:hover .block__hex {
        visibility: visible;
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
        visibility: hidden;
    }
}

.img__container {
    min-width: 40rem;
    min-height: 40rem;
    max-width: 40rem;
    max-height: 40rem;
    box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
        0 4px 6px -2px rgba(0, 0, 0, 0.05);
    border-radius: 1rem;
    img {
        border-radius: inherit;
        width: 100%;
        height: 100%;
        object-fit: cover;
        object-position: center;
    }
}

.image-info {
    display: flex;
    margin-left: -9rem;
}
</style>
