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

              <label class="label" for="name">Your Name:</label>

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

            <button >
              Submit
            </button>
          </form>
          
          <base-card>
          <ul v-for="user in userRatings" :key="user.id">
            <li>
              <span>{{ user.name }}</span> rating the learning experience
              <span> {{ user.feedback }}</span>
              <button @click ="getEditData(user)" class="mx-4">edit</button>
              <button @click ="deleteUserRating(user.id)" class="mx-4">delete</button>
            </li>
          </ul>
        </base-card>
          <div v-if="isEdit">
            <form @submit.prevent="submitEditForm">
            <the-view>
              <template v-slot:title>
                {{ this.editUserName }}
              </template>
              <template v-slot:description>
                 <h2 class="heading">My fanciness was </h2>

              <div>
                <input
                  type="radio"
                  name="rating"
                  id="rating-poor"
                  value="poor"
                  v-model="editRating"
                />
                <label class="label" for="rating-poor">Poor</label>
              </div>

              <div>
                <input
                  type="radio"
                  name="rating"
                  id="rating-avg"
                  value="average"
                  v-model="editRating"
                />
                <label class="label" for="rating-avg">Average</label>
              </div>

              <div>
                <input
                  type="radio"
                  name="rating"
                  id="rating-great"
                  value="great"
                  v-model="editRating"
                />
                <label class="label" for="rating-great">Great</label>
              </div>
              <p v-if="editRatingNotReady" class="text-red-500">
                Please choose your fanciness!
              </p>

            <button >
              Submit
            </button>
              </template>
            </the-view>
            </form>
          </div>
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
      ratingNotReady:false,
      url:'http://localhost:3000/userfaciness',
      userRatings:[],
      editAt: '',
      editUserName: '',
      editRating: null,
      isEdit: false,
      editRatingNotReady:false
    };
  },
  methods: {
    getEditData(EditInfo){
      this.isEdit = true
      this.editAt = EditInfo.id
      this.editUserName = EditInfo.name
      this.editRating = EditInfo.feedback
    },
    submitEditForm(){
      this.editRatingNotReady = this.editRating === null ? true:false
      if(!this.editRatingNotReady){
        this.putUserRating()
        this.isEdit = false
      }
    },
    submitForm(){
      this.nameNotReady = this.userName === '' ? true : false
      this.ratingNotReady = this.rating === null ? true : false 
      if(this.userName!== '' && this.rating !== null){
        this.postUserRatings({name:this.userName,rating:this.rating})
      }
      this.userName = ''
      this.rating = null
      
    },
    async getUserRatings(){
      try {
        const res = await fetch(this.url)
        const data = await res.json()
        return data;
        
        
      } catch (error) {
          console.log(`get error ${error}`)
      }
    },
    async postUserRatings(newUser){
      try {
        const res = await fetch(this.url,{
          method: 'POST',
          headers:{'content-type': 'application/json'},
          body: JSON.stringify({
            pictureid: this.obj.id,
            name: newUser.name,
            feedback: newUser.rating
          }
          )
        })
        const data = await res.json()
        this.userRatings = [...this.userRatings, data]
      } catch (error) {
          console.log(`get error ${error}`)
      }
    },
    async putUserRating(){
      try {
        const res = await fetch(`${this.url}/${this.editAt}`, {
          method: 'PUT',
          headers: {
            'content-type': 'application/json'
          },
          body: JSON.stringify({
            pictureid:this.obj.id,
            name: this.editUserName,
            feedback: this.editRating
          })
        })
        const data = await res.json()
        this.userRatings = this.userRatings.map((x) => 
        x.id === this.editAt
        ?{...x,feedback: data.feedback}:x )
      } catch (error) {
        console.log(`post error! ${error}`)
      }
    },
    async deleteUserRating(id) {
      try {
        await fetch(`${this.url}/${id}`, {
          method: 'DELETE'
        })
        this.userRatings = this.userRatings.filter(
          (x) => x.id !== id
        )
      } catch (error) {
        console.log(`delete error! ${error}`)
      }
    }
  },
  async created(){
    this.userRatings = await this.getUserRatings()
    this.userRatings = this.userRatings.filter(
      (x) => x.pictureid == this.obj.id
    )
  }
};
</script>