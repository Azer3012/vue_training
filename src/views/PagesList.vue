<template>
    <!-- <p>{{ counter }}</p> -->
    <p>{{ data.counter }}</p>
    <button @click.prevent="click">Click</button>
</template>

<script setup>

import {ref,reactive} from 'vue';


// const counter=ref(0);
const data=reactive({counter:0})

function click(){
    // counter.value++;
    data.counter++;
    
}



</script>