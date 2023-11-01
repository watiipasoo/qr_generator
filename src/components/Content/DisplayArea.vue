<template>
  <div class="qr-code-container">
    <h4 class="preview">PREVIEW</h4>
    <div class="code">
      <vue-qrcode ref="qrcode" :value="hello" :options="options"></vue-qrcode>
    </div>
    <p ref="DisplayError" class="error"></p>
    <div class="btn-container">
      <button class="generate-btn"
        @click="getinput(InputData, hexCode, hexCode2, InputData2, InputData3, selectedImage, this.$refs.qrcode.$el)">
        <span>Generate</span>
      </button>
      <button class="download-btn" @click="downloadQRCode">
        <span>Download</span>
      </button>
      <button class="print-btn" @click="printQRCodeAsPDF">
        <span>PDF</span>
      </button>
    </div>
  </div>
</template>


<script>
import VueQrcode from '@chenfengyuan/vue-qrcode'
import jsPDF from 'jspdf';

export default {
  components: { VueQrcode },
  props: ['InputData', 'hexCode', 'hexCode2', 'InputData2', 'InputData3', 'selectedImage'],
  data() {
    return {
      hello: "hello",
      options: {
        errorCorrectionLevel: 'Q',
        width: 400,
        maskPattern: 7,
        scale: 20,
        color: {
          dark: '#000000',
          light: '#ffffff',
        },
        margin: 0
      }
    }
  },
  mounted() {
    this.$refs.qrcode.scale = this.options.scale;
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
          const coverage = 0.25;
          const canvasWidth = canvas.width;
          const canvasHeight = canvas.height;

          const width = Math.round(canvasWidth * coverage);

          const imageAspectRatio = image.width / image.height;
          const height = width / imageAspectRatio;

          const imageX = (canvasWidth - width) / 2;
          const imageY = (canvasHeight - height) / 2;

          this.drawImage(context, image, imageX, imageY, width, height);
        };


        this.hello = InputData
        this.options.maskPattern = InputData2
        this.options.scale = InputData3
        this.options.color.dark = hexCode
        this.options.color.light = hexCode2
      } catch (error) {
        if (error.message === 'InputData is not defined') {
          this.$refs.DisplayError.textContent = "Enter URL!"
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
    drawImage(context, image, x, y, width, height) {
      context.shadowOffsetX = 0;
      context.shadowOffsetY = 0;
      context.shadowBlur = 0;
      context.shadowColor = '#00000040';
      context.lineWidth = 8;

      context.fillStyle = '#fff';
      context.fillRect(x, y, width, height);

      context.drawImage(image, x, y, width, height);
    },
    downloadQRCode() {
      try {
        if (!this.$refs.qrcode) throw new Error("QR code is not generated");

        const canvas = this.$refs.qrcode.$el;
        const link = document.createElement('a');
        link.href = canvas.toDataURL('image/png');
        link.download = 'qrcode.png';
        link.click();
      } catch (error) {
        console.error(error);
        // Handle the error, if necessary.
      }
    },
    printQRCodeAsPDF() {
      try {
        if (!this.$refs.qrcode) throw new Error("QR code is not generated");

        const canvas = this.$refs.qrcode.$el;
        const pdf = new jsPDF('p', 'mm', 'a4');
        pdf.addImage(canvas.toDataURL('image/png'), 'PNG', 10, 10, 90, 90);
        pdf.save('qrcode.pdf');
      } catch (error) {
        console.error(error);
      }
    }
  }
}
</script>

<style scoped>
/* Add styles for the QR code and its container */
.container {
  position: relative;
  margin-top: 20px;
}


.qr-code-container {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}

.error {
  color: red;
  font-weight: 600;
  font-size: medium;
}

.qr-code {
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
  border-radius: 8px;
  background: white;
}

.preview {
  font-weight: bold;
  font-size: 2rem;
  padding: 1rem;
}

.generate-btn {
  background: none;
  border: 1px solid #273775;
  padding: 1rem;
  color: #273775;
}

.download-btn {
  background: #273775;
  padding: 1rem;
  color: white;
}

.print-btn {
  background: #F9F871;
  padding-left: 2rem;
  padding-right: 2rem;
  color: black;
}

button {
  border-radius: 2rem;

  button:hover {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }
}

.btn-container {
  display: flex;
  gap: 2rem;
  justify-content: center;
  margin-top: 2rem;
}
</style>
