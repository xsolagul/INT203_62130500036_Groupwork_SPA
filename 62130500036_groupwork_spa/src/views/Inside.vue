<template>
  <the-view>
    <template v-slot:title> {{obj.title}}</template>
    <template v-slot:image>
      <img :src="require(`../assets/images/${obj.src}`)" 
      class="h-80 w-72 " />
    </template>
    <template v-slot:description>{{obj.explain}} </template>
  </the-view>
  
   <form @submit.prevent="submitForm">
            <base-card>
              <h2 class="heading">
                How was your fanciness?
              </h2>

              <label class="label" for="name">Your Name</label>

              <input
                class="input"
                id="name"
                type="text"
                v-model.trim="userName"
              />

              <p v-if="nameNotReady" class="text-red-500">
                Please enter your name!
              </p>
            </base-card>

            <base-card>
              <h2 class="heading">My fanciness was </h2>

              <div>
                <input
                  type="radio"
                  name="rating"
                  id="rating-poor"
                  value="poor"
                  v-model="rating"
                />
                <label class="label" for="rating-poor">Poor</label>
              </div>

              <div>
                <input
                  type="radio"
                  name="rating"
                  id="rating-avg"
                  value="average"
                  v-model="rating"
                />
                <label class="label" for="rating-avg">Average</label>
              </div>

              <div>
                <input
                  type="radio"
                  name="rating"
                  id="rating-great"
                  value="great"
                  v-model="rating"
                />
                <label class="label" for="rating-great">Great</label>
              </div>
              <p v-if="ratingNotReady" class="text-red-500">
                Please choose your fanciness!
              </p>
            </base-card>

            <button class="btn">
              Submit
            </button>
          </form>
</template>
<script>
import BaseCard from '../components/BaseCard.vue';
import TheView from "../components/TheView.vue";
export default {
  components: {
    TheView,
    BaseCard,
  },
  data() {
    return {
      obj: {
        id: this.$route.params.id,
        title: this.$route.params.title,
        explain: this.$route.params.explain,
        src: this.$route.params.src,
      },
      userName: '',
      rating:null,
      nameNotReady: false,
      ratingNotReady:false


    };
  },
  methods: {
    submitForm(){
      this.nameNotReady = this.userName === '' ? true : false
      this.ratingNotReady = this.rating === null ? true : false 
    }
  },
};
</script>