<template>

    <div class="p-2">
        <router-link v-bind:to="'/inside/' + information.id+'/'+information.title+'/'+information.explain+'/'+information.src" >{{information.title}}</router-link>
    </div>
</template>
<script>
export default {
    props:['information'],
    methods:{
        // sendId(){
        //     this.$emit('send-id', this.information.id)
        // }
    }
}
</script>