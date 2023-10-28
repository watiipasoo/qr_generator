<template>
  <div class="input-wrapper">
    <label>Enter URL</label>
    <input type="text" name="" required v-model="InputData" @input="handleInput('input-value', InputData)">
  </div>
</template>
<script>
export default {
  name: "ContentOne",
  data() {
    return { 
      InputData: ''
    }
  },
  methods: {
    handleInput(emitEvent, value) {
      this.$emit(emitEvent, value)
    }
  }
}
</script>

<style scoped>
.input-wrapper {
  position: relative;
  margin-bottom: 3rem;
}

input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  outline: none;
}

label {
  color: #000000;
  transition: all 0.3s ease-in-out;
  pointer-events: none;
  font-weight: 600;
  font-size: large;
}
</style>