<template>
  <the-view>
    <template v-slot:title> {{obj.title}}</template>
    <template v-slot:image>
      <img :src="require(`../assets/images/${obj.src}`)" 
      class="h-80 w-72 " />
    </template>
    <template v-slot:description>{{obj.explain}} </template>
  </the-view>
</template>
<script>
import TheView from "../components/TheView.vue";
export default {
  components: {
    TheView,
  },
  data() {
    return {
      obj: {
        id: this.$route.params.id,
        title: this.$route.params.title,
        explain: this.$route.params.explain,
        src: this.$route.params.src,
      },
    };
  },
  methods: {},
};
</script>