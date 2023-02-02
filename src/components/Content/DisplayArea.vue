<template>
    <vue-qrcode ref="qrcode" :value="hello" :options="options"></vue-qrcode>
    <p ref="DisplayError"></p>
    <div class="container"> <button
            v-on:click="getinput(InputData, hexCode, hexCode2, InputData2, InputData3, selectedImage, this.$refs.qrcode.$el)"><span>Generate
                code</span></button>
                </div>
</template>


<script>
import VueQrcode from '@chenfengyuan/vue-qrcode'

export default {
    components: { VueQrcode },
    props: ['InputData', 'hexCode', 'hexCode2', 'InputData2', 'InputData3', 'selectedImage'],
    data() {
        return {
            hello: "hello",
            options: {
                maskPattern: 7,
                scale: 4,
                color: {
                    dark: '#000000',
                    light: '#ffffff',
                },
                margin: 0
            }
        }
    },
    methods: {
        getinput(InputData, hexCode, hexCode2, InputData2, InputData3, selectedImage, canvas) {

            try {
                if (!InputData) throw new Error("InputData is not defined")
                const context = canvas.getContext('2d');
                const image = new Image();

                image.src = selectedImage;
                image.crossorigin = 'anonymous';
                image.onload = () => {
                    const coverage = 0.15;
                    const width = Math.round(canvas.width * coverage);
                    const x = (canvas.width - width) / 2;
                    console.log(canvas.width)

                    this.drawImage(context, image, x, x, width, width);
                };
                this.hello = InputData
                this.options.maskPattern = InputData2
                this.options.scale = InputData3
                this.options.color.dark = hexCode
                this.options.color.light = hexCode2
                // onReady()
            } catch (error) {
                if (error.message === 'InputData is not defined') {
                    this.$refs.DisplayError.textContent = "Input is empty"
                    setTimeout(() => {
                        this.$refs.DisplayError.textContent = ""
                    }, 2000)
                    console.log("error: no input text")
                } else {
                    console.log(error)
                    this.error = error.message
                }
            }

        },
        // onReady(canvas) {
        // },
        drawImage(context, image, x, y, width, height, radius = 4) {
            context.shadowOffsetX = 0;
            context.shadowOffsetY = 2;
            context.shadowBlur = 4;
            context.shadowColor = '#00000040';
            context.lineWidth = 8;
            context.beginPath();
            context.moveTo(x + radius, y);
            context.arcTo(x + width, y, x + width, y + height, radius);
            context.arcTo(x + width, y + height, x, y + height, radius);
            context.arcTo(x, y + height, x, y, radius);
            context.arcTo(x, y, x + width, y, radius);
            context.closePath();
            context.strokeStyle = '#fff';
            context.stroke();
            context.clip();
            context.fillStyle = '#fff';
            context.fillRect(x, x, width, height);
            context.drawImage(image, x, x, width, height);
        },
    }
}
</script>

<style scoped>
*,
*:after,
*:before {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
}

@import url('https://fonts.googleapis.com/css2?family=Nunito+Sans:wght@200&display=swap');

:root {
    --font-style: 'Nunito Sans', sans-serif;
}

* {
    box-sizing: border-box;
}

.container {
    position: relative;
    margin-top: 20px;
}

button {
    display: inline-block;
    position: relative;
    background: none;
    border: none;
    color: #fff;
    font-size: 18px;
    cursor: pointer;
    background: #18181B;
}

span {
    display: block;
    padding: 25px 80px;
}

button::before,
button::after {
    content: "";
    width: 0;
    height: 2px;
    position: absolute;
    transition: all 0.2s linear;
    background: #54E6E7;
}

span::before,
span::after {
    content: "";
    width: 2px;
    height: 0;
    position: absolute;
    transition: all 0.2s linear;
    background: #54E6E7;
}

button:hover::before,
button:hover::after {
    width: 100%;
}

button:hover span::before,
button:hover span::after {
    height: 100%;
}

button::after {
    right: 0;
    bottom: 0;
    transition-duration: 0.4s;
}

button span::after {
    right: 0;
    bottom: 0;
    transition-duration: 0.4s;
}

button::before {
    left: 0;
    top: 0;
    transition-duration: 0.4s;
}

button span::before {
    left: 0;
    top: 0;
    transition-duration: 0.4s;
}
</style>