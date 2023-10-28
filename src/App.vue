<template>
  <div class="out-wrapper">
<ParentComponent/>
  </div>
  
</template>

<script>
import ParentComponent from './components/ParentComponent.vue';



export default {
  name: 'App',
  components: {
    ParentComponent
  }
}
</script>

<style>
body{
  margin: 0;
}
.out-wrapper{
  display: flex;
  gap:2rem;
  flex-direction: column;
  padding: 2rem;
  /* Style the scrollbar and its thumb */
  scrollbar-width: thin; /* Firefox */
  scrollbar-color: #ff0000 #f0f0f0; /* Firefox */
}
</style>
