<script setup>
import HelloWorld from '@/components/HelloWorld.vue';
import TheWelcome from '../components/TheWelcome.vue'
import {computed, onMounted, ref} from 'vue'
import { useRouter } from 'vue-router';
import path from 'path';
const count = ref(10);
const test = ref('gg');
const handleIncrease = (data) => {
  test.value = data.name;
  console.log(test);
  count.value = count.value + data.value;

}

const categoryProduct = ref('food');


const products = ref([
 {
  id: 1,
  name:'pizza',
  category: 'food',
  price:500
 },
 {
  id: 2,
  name:'cake',
  category: 'food',
  price:400
 },
 {
  id: 3,
  name:'coca',
  category: 'drink',
  price:50
 },
 {
  id: 4,
  name:'pessi',
  category: 'drink',
  price:500
 },
]);


const handleChangeCategoryProduc = (value) => {
  categoryProduct.value = value
};


const productFilter = computed(() => {
  return products.value.filter(item => item.category === categoryProduct.value)
})

const users = ref([])
const txt_search = ref('');
onMounted(() => {
  fetch('https://jsonplaceholder.typicode.com/users')
      .then(response => response.json())
      .then(json => users.value = (json))
}) 

const filterUser = computed (() => {
  return users.value.filter(item => item.name.toUpperCase().indexOf(txt_search.value.toUpperCase()) != -1 
                                    || item.email.toUpperCase().indexOf(txt_search.value.toUpperCase()) != -1)
})

const router = useRouter();
</script>

<template>
  <main>

   
    <input class="search_work" placeholder="search work here" v-model="txt_search"></input>
    <div class="group_card">
      <div class="card_item" v-for="user in filterUser">
        <div @click="router.push({path: `todo/${user?.id}`})">
          <h2 class="name_card_item">{{user.name}}</h2>
          <i>{{ user.email }}</i>
        </div>
      </div>
     
    </div>
 
    <!-- <TheWelcome :countView="count" @handle-increase="handleIncrease"/> -->
<!-- <button @click="handleChangeCategoryProduc('food')"> Hien thi food </button>
<button @click="handleChangeCategoryProduc('drink')"> Hien thi drink </button>

<div v-if="categoryProduct === 'food'">Danh sach Food</div>
<div v-else-if="categoryProduct === 'drink'">Danh sach Drink</div>

<div v-for="product in productFilter" >
  <div class="group_product_item">
    <div>{{ product.name }} {{ product.price }}</div>
  </div>
</div> -->

  </main>
</template>

<style>
.search_work{
  margin-top: 20px;
  width: 100%;
  border-radius: 50px;
  background: #ededed;
  padding: .6rem 1.2rem;
  border: none;
  outline: none;
  

}

.group_card{
  margin-top: 1.5rem;
  display: flex;
  flex-direction: column;
  row-gap: 1.5rem;
}
.card_item{
  border-radius: 10px;
  background: #323232;
  color: #fff;
  cursor: pointer;
  padding: .6rem 1.2rem;
  box-shadow: 1px 1px 10px rgba(0,0,0,0.15);

}
</style>
