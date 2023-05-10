<template>
  <div :class="display ? 'loader' : 'd-none' "></div>
    <div :class="{ 'bg-women': product.category == 'women\'s clothing', 'bg-men': product.category == 'men\'s clothing', 'd-none': display }">

    <div class="product-page" v-if="product.category == 'men\'s clothing' || product.category == 'women\'s clothing'">
      <div class="img-container">
        <img :src="product.image" :alt="product.title" />
      </div>
    
      <div class="desc-container">
        <p class="product-title" >{{ product.title }}</p>
    
        <div class="product-rating">
          <p>{{ product.category }}</p>
          <div class="rating">
            <p>
              {{ product.rating.rate }} / 5

            </p>
            <span v-for="n in 5" :class="{ 'circle-filled-men': product.category == 'men\'s clothing' && n  <= product.rating.rate, 'circle-filled-women': product.category == 'women\'s clothing' && n  <= product.rating.rate, 'circle-empty-men': product.category == 'men\'s clothing' && n > product.rating.rate, 'circle-empty-women': product.category == 'women\'s clothing' && n > product.rating.rate }"></span>
          </div>
        </div>
    
        <p class="product-desc">{{ product.description }}</p>
    
        <div>
          <p class="product-price">${{ product.price }}</p>
          <div>
            <button  type="submit" :class="product.category == 'women\'s clothing' ? 'btn-buy-women' : (product.category == 'men\'s clothing' ? 'btn-buy-men' : 'btn-buy-empty')">Buy now </button>
            <button @click="fetchProduct" type="submit" :class="product.category == 'women\'s clothing' ? 'btn-next-women' : (product.category == 'men\'s clothing' ? 'btn-next-men' : 'btn-next-empty')">Next Product</button>
          </div>
        </div>
      </div>
    </div>

    <div :class="display ? 'd-none' : 'bg-empty'" v-else>
      <div class="empty-page">
        <p>This product is unavailable to show</p>
        <button @click="fetchProduct">Next product</button>
      </div>
    </div>
  </div>
</template>
  
<script>
  export default {
    data() {
      return {
        product: {},
        index: 1,
        display:true,
      };
    },
    methods: {
      async fetchProduct() {
        const response = await fetch(`https://fakestoreapi.com/products/${ this.index <= 20 ? this.index++ : this.index = 1 }`);
        const data = await response.json();
        this.product = data;
        this.display = false;
      },
    },
    mounted() {
      this.fetchProduct();
    },
  };
</script>

<style src="../../assets/style/page.css"></style>