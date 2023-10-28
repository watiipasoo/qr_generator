<template>
  <div class="wrapper">
    <div class="w-container">
      <div class="top-bar">
        <img src="../assets/logo.png" alt="Your Title Image" class="title-image">
        <ul>
          <li><a href="/">Help</a></li>
        </ul>
      </div>
      <h2 class="centered-title">Quick QR-Code</h2>
      <ContentOne v-on:input-value="updateValue" />
      <div class="container">
        <div>
          <ContentTwo v-on:input-value2="updateValue2" v-on:input-value3="updateValue3" v-on:input-value4="updateValue4"
            v-on:input-value5="updateValue5" />
          <ContentThree @selected="setSelectedImage" />
        </div>
        <div class="display-area">
          <DisplayArea :InputData="InputData" :InputData2="InputData2" :InputData3="InputData3" :hexCode="hexCode"
            :hexCode2="hexCode2" :selectedImage="selectedImage" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ContentOne from './Content/ContentOne.vue';
import ContentTwo from './Content/ContentTwo.vue';
import ContentThree from './Content/ContentThree.vue';
import DisplayArea from './Content/DisplayArea.vue';


export default {
  name: 'HelloWorld',
  components: {
    ContentOne,
    ContentTwo,
    ContentThree,
    DisplayArea
  },
  data() {
    return {
      InputData: '',
      hexCode: '',
      hexCode2: '',
      InputData2: '',
      InputData3: '',
      selectedImage: '',
      items: [
        { id: 1, title: 'ENTER CONTENT', content: 'This is the content of item 1' },
        { id: 2, title: 'CUSTOMIZE', content: 'This is the content of item 2' },
        { id: 3, title: 'ADD LOGO', content: 'This is the content of item 3' },
        { id: 3, title: 'DISPLAY', content: 'This is the content of item 4' },
      ],
      selectedItem: null
    }
  },
  methods: {
    updateValue(value) {
      this.InputData = value
    },
    updateValue2(value) {
      this.hexCode = value
    },
    updateValue3(value) {
      this.hexCode2 = value
    },
    updateValue4(value) {
      this.InputData2 = value
    },
    updateValue5(value) {
      this.InputData3 = value
    },
    setSelectedImage(selectedImage) {
      this.selectedImage = selectedImage;
    },
    showContent(item) {
      this.selectedItem = item
    },
  },
  emits: ['Selected']
}
</script>

<style scoped>
.container {
  display: flex;
  gap: 4rem;
  justify-content: center;
}

.wrapper {
  display: flex;
  justify-content: center;
}

.top-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 3rem;
}

.display-area {
  border: 2px solid #273775;
  padding: 2rem;
  border-radius: 1rem;
}

.title {
  font-size: 36px;
  color: #273775;
  margin: 4px 0;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 2px;
}
.centered-title {
  text-align: center;
  padding-top: 1rem; 
  padding-bottom: 3rem;
  font-size: 2rem;
  font-weight: 800;
}
</style>
