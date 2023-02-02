<template>
  <div>
    <ul>
      <li v-for="item in items" @click="showContent(item)" :key="item.id" :class="{ active: item === selectedItem }">{{
        item.title
      }}</li>
    </ul>
    <div class="content" v-show="selectedItem === items[0]">
      <ContentOne v-on:input-value="updateValue" />
    </div>
    <div class="content" v-show="selectedItem === items[1]">
      <ContentTwo v-on:input-value2="updateValue2" v-on:input-value3="updateValue3" v-on:input-value4="updateValue4"
        v-on:input-value5="updateValue5" />
    </div>
    <div class="content" v-show="selectedItem === items[2]">
      <ContentThree @selected="setSelectedImage" />
    </div>
    <div class="content" v-show="selectedItem === items[3]">
      <DisplayArea :InputData="InputData" :InputData2="InputData2" :InputData3="InputData3" :hexCode="hexCode"
        :hexCode2="hexCode2" :selectedImage="selectedImage" />
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
ul {
  margin: 5% 5% 2% 5%;
  display: flex;
  flex-direction: row;
  list-style: none;
  padding: 25px 0;
  border-radius: 25px;
  border: 0.1px solid #099FFF;
  background-color: #18181B;
  box-shadow: 0 4px 8px 0 #00FFFF, 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

li {
  margin: auto;
  font-size: 20px;
  cursor: pointer;
}

li::after {
  display: block;
  content: '';
  border-bottom: solid 1px #00FFFF;
  padding-bottom: 1%;
  transform: scaleX(0);
  transition: transform 300ms ease-in-out;
}

li:hover::after {
  transform: scaleX(1);
}

.content {
  border-radius: 25px;
  margin: 0 5% 0 5%;
  padding: 25px 0;
  background: #2B3241;
  box-sizing: border-box;
  justify-content: center;
  align-items: center;
}
</style>
