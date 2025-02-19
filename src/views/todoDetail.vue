<script setup>
import { useRoute } from 'vue-router';
import {onMounted, ref}  from 'vue'
 const router = useRoute();
const user = ref(null);


 onMounted(() => {
  fetch(`https://jsonplaceholder.typicode.com/users/${router.params.id}`)
      .then(response => response.json())
      .then(json => user.value = (json))
}) 
</script>
<template>
    <div class="card_item" >
        
          <h3>{{user?.name}}</h3>
        
          <h5>{{user?.website}}</h5>
          <h6>{{user?.phone}}</h6>

    </div>
  </template>
  
  <style>
  @media (min-width: 1024px) {
    .about {
      min-height: 100vh;
      display: flex;
      align-items: center;
    }
  }
  </style>
  