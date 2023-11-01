<template>
  <div class="gradient-input">
    <div>
      <label for="colorInput">Fore Ground Color:</label>
      <input type="color" v-model="hexCode" @input="handleInput('input-value2', hexCode)">
      <input type="text" v-model="hexCode" @input="handleInput('input-value2', hexCode)">
    </div>
    <div>
      <label for="colorInput">Background Color:</label>
      <input type="color" v-model="hexCode2" @input="handleInput('input-value3', hexCode2)">
      <input type="text" v-model="hexCode2" @input="handleInput('input-value3', hexCode2)">
    </div>
    <div>
      <label>MaskPattern:</label>
      <input type="number" v-model.number="MaskPattern" min="0"
        @input="handleMPInput('input-value4', MaskPattern)" />
    </div>
    <!-- <div>
      <label>Size: </label>
      <input type="number" v-model.number="Scale" min="0"
        @input="handleScaleInput('input-value5', Scale)" />
    </div> -->
  </div>
</template>

<script>
export default {
  name: "ContentTwo",
  emits: ['input-value2', 'input-value3', 'input-value4', 'input-value5'],
  data() {
    return {
      hexCode: '#000000',
      hexCode2: '#ffffff',
      MaskPattern: 4,
      Scale: 15,
    }
  },
  methods: {
    handleInput(emitEvent, value) {
      this.$emit(emitEvent, value)
    },
    handleMPInput(emitEvent, value) {
      this.$emit(emitEvent, value)
    },
    handleScaleInput(emitEvent, value) {
      this.$emit(emitEvent, value)
    }
  }
}
</script>

<style scoped>
.gradient-input {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.input-group {
  display: flex;
  gap: 10px;
}

.input-wrapper {
  display: flex;
  align-items: center; /* Vertically center the input field */
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 5px;
}

input[type="number"] {
  width: 50px; /* Adjust the width as needed */
  border: none;
  outline: none;
}

label {
  font-weight: bold;
  margin-right: 5px;
}

span {
  margin-left: 5px;
}
</style>
