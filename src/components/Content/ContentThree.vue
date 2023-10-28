<template>
     <div class="images-container">
        <img v-for="(imgSrc, index) in imgSrcList" :src="imgSrc" :key="index"
            @click="selectImage(imgSrc, index)" :class="{ thumbnail: selectedIndex === index }" />
    </div>
    <div class="drag-area" ref="dropArea">
        <div class="icon"><i class="fas fa-cloud-upload-alt"></i></div>
        <header ref="dragText">Drag & Drop to Upload File</header>
        <span>OR</span>
        <button @click="openFilePicker">Browse File</button>
        <input type="file" hidden ref="input" multiple />
    </div>
   
</template>

<script>
export default {
    data() {
        return {
            imgSrcList: [],
            selectedIndex: -1
        }
    },
    computed: {
        selectedImage() {
            return this.imgSrcList[this.selectedIndex];
        }
    },
    methods: {
        selectImage(selectedImage, index) {
            this.selectedIndex = index;
            this.$emit('Selected', selectedImage);
            console.log(this.imgSrcList)
        },
        openFilePicker() {
            this.$refs.input.click()
        },
        handleFileChange(event) {
            let file = event.target.files[0]
            let validExtensions = ["image/jpeg", "image/jpg", "image/png"
            ];
            let fileType = file.type
            if (validExtensions.includes(fileType)) {
                let fileReader = new FileReader();
                fileReader.onload = (e) => {
                    this.imgSrcList.push(e.target.result)
                    console.log(fileReader.result);
                    this.$refs.dropArea.classList.remove("active");
                    this.$refs.dragText.textContent = "The file is successfully uploaded."
                    setTimeout(() => {
                        this.$refs.dragText.textContent = "Drag & Drop to Upload File"
                    }, 2000)
                }
                fileReader.readAsDataURL(file);
                this.openFilePicker();
            } else {
                this.$refs.dropArea.classList.remove("active");
                this.$refs.dragText.textContent = "This is not an valid file!"
                setTimeout(() => {
                    this.$refs.dragText.textContent = "Drag & Drop to Upload File"
                }, 2000)
            }
        },
        handleDragOver(event) {
            event.preventDefault();
            this.$refs.dropArea.classList.add("active");
            this.$refs.dragText.textContent = "Release to Upload File";
        },
        handleDragLeave() {
            this.$refs.dropArea.classList.remove("active");
            this.$refs.dragText.textContent = "Drag & Drop to Upload File";
        },
        handleDrop(event) {
            event.preventDefault();
            let file = event.dataTransfer.files[0];
            this.handleFileChange({ target: { files: [file] } });
        },
    },
    mounted() {
        this.$nextTick(() => {
            this.$refs.dropArea.addEventListener("dragover", this.handleDragOver);
            this.$refs.dropArea.addEventListener("dragleave", this.handleDragLeave);
            this.$refs.dropArea.addEventListener("drop", this.handleDrop);
            this.$refs.input.addEventListener("change", this.handleFileChange);
        });
    }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;500;600;700&display=swap');

.thumbnail {
    border: 2px solid blue;
}

img {
    margin: 10px 10px 0 20px;
    cursor: pointer;
}

.drag-area {
    border: 2px dashed #1b1b1b;
    padding: 10px;
    margin-top: 1rem;
    border-radius: 5px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
}

.drag-area.active {
    border: 10px dashed #B92C2C;
}

.icon {
    font-size: 100px;
}

header {
    font-size: 15px;
    font-weight: 500;
}

span {
    font-size: 20px;
    font-weight: 500;
    margin: 10px 0 15px 0;
}

button { padding: 1rem;
    font-weight: 500;
    border: none;
    outline: none;
    background: #000000;
    color: #ffffff;
    border-radius: 5px;
    cursor: pointer;
}
</style>
