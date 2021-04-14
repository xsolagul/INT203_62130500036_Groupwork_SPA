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
         title: 'บรีซเอกเซล คัลเลอร์ สูตรใหม่' ,
         explain: 'สูตรเข้มขัน คงความสดใส ให้ผ้าสี',
         src:'1.jpg'
        },
        {
          id:2,
         title: 'บรีซเอกเซล comfort' ,
         explain: 'สูตรเข้มขัน หอมยาวนาน 4สัปดาห์',
         src:'2.jpg'
        },
        {
          id:3,
         title: 'บรีซเอกเซล แอคทีฟเฟรช' ,
         explain: 'สยบกลิ่นกระจายความหอม',
         src:'3.jpg'
        },
        {
          id:4,
         title: 'บรีซเอกเซล โกลด์' ,
         explain: 'สูตรเข้มข้น ฟองพอเหมาะ ถนอมเครื่องฝาหน้า',
         src:'4.jpg'
        },
        {
          id:5,
         title: 'บรีซเอกเซล' ,
         explain: 'ขจัดคราบที่มองเห็นและมองไม่เห็น',
         src:'5.jpg'
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
