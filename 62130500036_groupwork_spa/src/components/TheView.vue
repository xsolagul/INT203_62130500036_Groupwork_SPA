<template>
    <base-card>
    <h1 class="text-xl text-left">
    <slot name="title"></slot>
    </h1>
    <slot name="image" ></slot>
    <slot name="description"></slot>
    </base-card>
</template>
<script>
export default {
    methods:{
    }
}
</script>