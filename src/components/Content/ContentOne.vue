<template>
  <div>
    <input type="text" name="" required v-model="InputData" @input="handleInput('input-value', InputData)">
    <label>Enter Content</label>
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
@import url('https://fonts.googleapis.com/css2?family=Nunito+Sans:wght@200&display=swap');

:root {
  --font-style: 'Nunito Sans', sans-serif;
}

* {
  box-sizing: border-box;
}

body {
  background: #131315;
  font-family: var(--font-style);
}


input {
  position: relative;
  width: 100%;
  padding: 10px 0;
  font-size: 16px;
  color: #00FFFF;
  margin-bottom: 30px;
  text-align: center;
  border: none;
  border-bottom: 2px solid #00FFFF;
  outline: none;
  background: transparent;
}

label {
  position: relative;
  left: 0;
  top: -60px;
  padding: 10px 0;
  font-size: 20px;
  pointer-events: none;
  transition: .5s;
}

input:focus~label,
input:valid~label {
  top: -85px;
  left: 0;
  color: #099FFF;
  font-size: 16px;
}
</style>
