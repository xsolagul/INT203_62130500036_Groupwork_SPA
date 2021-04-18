<template>
<div v-for="obj in this.allPicInfo" :key="obj.id">
<the-view>
      <template v-slot:title> {{obj.title}}</template>
    <template v-slot:image>
      <img :src="require(`../assets/images/${obj.src}`)" 
      class="h-80 w-72 " />
    </template>
    <template v-slot:description> has great feedback = {{ obj.countGreat }} <br/>
  has average feedback ={{ obj.countAverage}} <br/>
  has Poor feedback ={{obj.countPoor}}</template>

</the-view>
</div>

</template>
<script>
import TheView from "../components/TheView.vue";
export default {
  components: {
    TheView,
  },
  data() {
    return {
      allInformation: [],
      allPicInfo:[],
      url: "http://localhost:3000/userfaciness",
      picUrl: "http://localhost:3000/item" ,
      allFeedbackId:[]
    };
  },
  methods: {
      getGreatFeedback(id){
        let countGreat = 0
        let countAverage = 0
        let countPoor = 0
          for (let index = 0; index < this.allInformation.length; index++) {
              if(id == this.allInformation[index].pictureid){
              if(this.allInformation[index].feedback=="great"){
                  countGreat = countGreat + 1
              }  
              if(this.allInformation[index].feedback=="poor"){
                  countPoor = countPoor + 1
              }  
              if(this.allInformation[index].feedback=="average"){
                  countAverage = countAverage + 1
              }  
              }
          }this.allFeedbackId.push({picId:id,countGreat:countGreat,countAverage:countAverage,countPoor:countPoor})
          this.allPicInfo[id-1].countGreat = countGreat
          this.allPicInfo[id-1].countAverage = countAverage
          this.allPicInfo[id-1].countPoor = countPoor
          },
    async getAlldata() {
      try {
        const res = await fetch(this.url);
        const data = await res.json();
        return data;
      } catch (error) {
        console.log(`get error ${error}`);
      }
    },
    async getPicdata(){
      try {
        const res = await fetch(this.picUrl);
        const data = await res.json()
        return data;
      } catch (error) {
        `get error ${error}`
      }
    }    

  },
  async created(){
      this.allInformation = await this.getAlldata()
      this.allPicInfo = await this.getPicdata()
      for (let index =1 ; index < this.allPicInfo.length+1; index++){
          this.getGreatFeedback(index)
      }
  }
};
</script>