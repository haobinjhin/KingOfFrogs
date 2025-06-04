<script setup>

const props = defineProps({
    name: {
        type: String,
        required: true,
    },
    type1: {
        type: String,
        required: true
    },
    type2: {
        type: String,
        default: null
    },
    hp: {
        type: Number,
        required: true,
    },

})

</script>

<template>
    <div class="Cards">
        <h1>{{ name }}</h1>
        <h2>{{ type1 }}</h2>
        <h2 v-if="type2">{{ type2 }}</h2>
        <h2>{{ hp }}</h2>
    </div>
  
</template>

<style scoped>

</style>