<template>
    <h1>TẤT CẢ SẢN PHẨM</h1>
    <Product v-for="item in filterproduct" :key="item.id" :product="item"/>

    <!-- Nút lùi -->
  <button v-if="currentpage>1" @click="changepage(currentpage-1)">Prev</button>
  <p v-for="i in totalpage" :key="i">
      <button @click="changepage(i)">{{i}}</button>
  </p>
  <!-- Nút tới -->
  <button @click="changepage(currentpage+1)">Next</button>
  <p>{{currentpage}} of {{totalpage}}</p>

</template>
  
  <script>
  import Product from './ComProduct.vue'
  import items from '../data/items.js'
  export default {
      name:'ComHome',
      components:{
        Product
      },
      data(){
        return{
          products:items,
          //Phân trang
          currentpage:1,
          limit:4
        }
      },
      computed:{
      totalpage()
      {
        return Math.ceil(this.products.length/this.limit)
      },
      filterproduct()
      {
        const start=(this.currentpage-1)*this.limit
        const end=start+this.limit
        return this.products.slice(start,end)
      }
    },
    methods:{
      changepage(page)
      {
        if(page >=1 && page<=this.totalpage)
        {
          this.currentpage=page
          console.log(this.currentpage)
        } 
      }
    }
  }
  </script>
  
  <style>
  
  </style>