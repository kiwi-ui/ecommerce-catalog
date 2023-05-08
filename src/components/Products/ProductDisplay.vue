<template>
    <div>
      <h1>{{ product.title }}</h1>
      <img :src="product.image" :alt="product.title" />
      <p>{{ product.description }}</p>
    </div>
    <button @click="fetchProduct">Next</button>
  </template>
  
  <script>
  export default {
    data() {
      return {
        product: {},
        index: 1,
      };
    },
    methods: {
    async fetchProduct() {
          const response = await fetch(`https://fakestoreapi.com/products/${ this.index <= 20 ? this.index++ : this.index = 1 }`);
          const data = await response.json();
          
          if(data.category == "men's clothing" || data.category == "women's clothing" ) {
              this.product = data;
              console.log(data)
            }
            else {  }
    },
  },
    mounted() {
      this.fetchProduct();
    },
  };
  </script>
  