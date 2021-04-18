<template class="bg-gray-600">

  <div id="nav" class="bg-green-400">
    <div class ="items-center space-x-8 px-8 py-2 w-full ">
    <router-link to="/">Home</router-link> 
    <router-link to="/about">About</router-link>
    <router-link to="/Status">Allstatus</router-link>
  </div>
  </div>
 
  <router-view class=""/>
  <div class="bg-gray-600 bg-no-repeat bg-ce" style="background "> </div>
</template>

<script>

export default {
  data() {
   
  },
}
</script>
