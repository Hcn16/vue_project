<script setup>
import { RouterLink, RouterView } from 'vue-router'
import { provide, ref } from 'vue';

const test_provide = ref(0)
provide('test_provide', test_provide)
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="60" height="60" />

    <div class="wrapper">

      <nav>
        <RouterLink to="/">
          <div class="btn-main">Home</div></RouterLink>
        <RouterLink to="/create">
          <div class="btn-action">Create</div></RouterLink>
      </nav>
    </div>
  </header>

 

  <RouterView />

</template>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  padding: .4rem 2rem;
  align-items: center;
  box-shadow: 1px 1px 10px rgba(0, 0, 0, 15);
 
}

nav{
  display: flex;
  column-gap: 1rem;
}





@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
