<template>
    <button @click="buttonClick" class="p-1 m-2 " :class ="[bgcolor, txtcolor]">
    {{label}}
    </button>
</template>
<script>
export default {
    props: ['bgcolor','txtcolor','label'],
    emits: ['btn-click'],
    methods: {
        buttonClick(){
            this.$emit('btn-click',this.label)
        }
    }
}
</script>