<template>
  
  <div class="bg-[#3498db] text-white p-4 rounded-md">
    <h1 class="text-center text-xl md:text-3xl font-bold">To-do-list</h1>
</div>

  <div class="p-4">
    <router-view/>
    <!-- class="bg-[#EAEDED]" -->
  </div>
</template>

<script>
  export default{
    name:'App'
  }
</script>

<style scoped></style>
