<template>
  <the-list @send-id='getId' v-for="information in  informations" 
  :key=information.id :information="information"
   >
  </the-list>
</template>

<script>
// @ is an alias to /src

import TheList from '../components/TheList.vue'
export default {
  name: 'Home',
  components: {
   
    TheList
  },
data(){
    return { 
     informations: [
       {
         id: 1,
         title: 'dsad' ,
         explain: 'dsadsa',
         src:'dsadassad'
        },
        {
          id:2,
         title: 'dsad' ,
         explain: 'dsadsa',
         src:'dsadassad'
        },
        {
          id:3,
         title: 'dsad' ,
         explain: 'dsadsa',
         src:'dsadassad'
        },
        {
          id:4,
         title: 'dsad' ,
         explain: 'dsadsa',
         src:'dsadassad'
        },
        {
          id:5,
         title: 'dsad' ,
         explain: 'dsadsa',
         src:'dsadassad'
        }
     ],
     itemclicked: 0 ,
    }
  } ,
  methods:{
    getId(id){
      this.itemclicked = id
      console.log(this.itemclicked)
    }
  }
}
</script>
